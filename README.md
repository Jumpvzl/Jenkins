# Jenkins
Tutorial Jenkins DevSecOps


Este Tutorial tiene como base principal, especificar los pasos de DevSecOps utilizando Jenkins todos los pipeline estan realizados mediante software de código abierto.




######## DOCKER #######

1.- utilizamos el siguiente repositorio https://github.com/Jumpvzl/dockerjenkins.git
Editamos el archivo docker-compose.yml

version: '3'
services:
  jenkins:
    image: jenkins/docker
    build:
     context: dockerjenkins
    ports:
    - 8080:8080
    - 50000:50000
    container_name: jenkins
    volumes:
      - $PWD/jenkins_home:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
    networks:
      - net
networks:
  net:

hacemos un stop luego de las configuraciones docker-compose stop
compilamos la nueva imagen local docker-compoose build

Esperamos el proceso.......

habilitamos los permisos para que el usuario jenkins pueda ejecutar docker
- docker exec -it --user root jenkins bash
- chown jenkins /var/run/docker.sock

volvemos a entrar con jenkins

docker exec -it jenkins bash


############# Ejercicio con NodeJS ####################

Instalamos el plugin NodeJS

Configuramos la Global Tool Configuration para NodeJS

Nombre y ultima version actualizada

clonar el repo NodeJS https://github.com/Jumpvzl/NodeJS.git

Creamos la tarea -> Aplicacion NodeJS
Proyecto Estilo Libre
LLenamos la descripcion

origen del codigo fuente -> GIT utilizamos el repo -> https://github.com/Jumpvzl/NodeJS.git


Seccion de Build o Ejecucion:
Seleccionamos comandos Shell
npm install 

Seleccionamos en Entorno de Ejecucion "Provide Node & npm bin/folder to PATH"

Guardar

PASO SIGUIENTE EMPAQUETAR LA APP NODEJS EN IMAGEN DE DOCKER Y PUBLICARLA EN DOCKERHUB

Se instala el PLUGIN -> CloudBees Docker Build and Publish

se configura en la seccion de build o ejecutar - "Docker Build and Publis" 

Se asigna un nombre del repositorio: se debe crear primero en dockerhub el repositorio como publico!!!!

se asigna un tag en caso contrario por defecto se llena el lastest

se debe llenar las credenciales del dockerhub dentro de jenkins - solamente se agregan usuario / contraseña

se descarga la imagen de docker y se ejecuta
- docker pull jumpvzl/NodeJS
- docker run -p 3000:3000 -d --name nodejsapp jumpvzl/NodeJS

compruebas su ejecucion 

curl localhost:3000


