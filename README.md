# MEAN-Docker

## Introduction
**Docker -** A containerization platform that packages your application and all its dependencies together in the form of a docker container to ensure that your application works seamlessly in any environment.
Containerizing a single service application is easy. But what if we had to containerize multiple services in separate containers.
**Docker Compose** can be used to create separate containers (and host them) for each of the stacks in a MEAN stack application. MEAN is the acronym for MongoDB, Express, Angular & NodeJs.
By using Docker Compose, we can host each of these technologies in separate containers on the same host and get them to communicate with each other. Each container will expose a port for communicating with other containers.
The communication and up-time of these containers will be maintained by Docker Compose.

## About the Project
This is simple MEAN Stack app containerized using Dockerfile and Docker-compose in which I have used Angular for the frontend, Express Server for the backend and MongoDB as database. 

## Requirements to work with this project.
You need to have **Docker**(preferably Version- 19.03.8) and **Docker Compose** in your system to run and work with this project.
Instruction to install Docker can be [found here](https://docs.docker.com/engine/install/).
Instruction to install Docker-Compose can be [found here](https://docs.docker.com/compose/install/).

## The Project
This project contain two directory/folder named as "angular-app" for the frontend and "express-server" for the backend and a docker-compose with the name "docker-compose.yml".

#### angular-app/Dockerfile
```
FROM node:12.16-alpine3.9
RUN mkdir -p /app
WORKDIR /app
COPY package.json /app/
RUN npm install
RUN npm install -g @angular/cli
COPY . /app/
EXPOSE 4200
CMD ["npm", "start"]
```
#### express-server/Dockerfile
```
FROM node:12.16-alpine3.9
RUN mkdir -p /app
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app/
EXPOSE 3000
CMD ["npm", "start"]
```
#### docker-compose.yml
```
version: '3'

services:
  angular:
    build: angular-app
    ports:
      - "4200:4200"
    volumes:
      - ./angular-app:/app

  express:
    build: express-server
    ports:
      - "3000:3000"
    links:
      - database

  database:
    image: mongo
    ports:
      - "27017:27017"

```

#### Using this project
First download and install Docker and Docker-Compose on your host system them download or clone the structure on your system in a directory(termed as root directory for this application). Once the structure is cloned, change your directory to the application root directory and run the command -
```
$ docker-compose up --build -d
```
Here "build" parameter is used to build the image we defined in Dockerfile if it does not exists already and  "-d" flag is used run the command in background which is voluntry.

Once the process is done means the containers are hosted, you can see the services active on their respective ports. Go to your browser and search for -
- **localhost:4200** - Angular App
- **localhost:3000** - Express Server & NodeJs
- **localhost:27017** - MongoDB

Thank You.
