## Docker Overview

https://www.lynda.com/Docker-tutorials/Docker-Developers/2211315-2.html?org=bpl.org

- install: https://docs.docker.com/engine/install/ubuntu#install-using-the-repository

Container
Image: blueprint / instructions for the container, defined in `Dockerfile`

```docker
// Dockerfile
FROM node

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 4000

CMD [ "npm", "start"]
```

- create image: `➜ backend sudo docker build -t <owner/image-name> .`

```bash
➜  backend sudo docker build -t demo/simple-backend .
```

- view images: `➜ backend sudo docker images`
- remove an image (w/ force) `➜ backend sudo docker rmi -f <image id>`

- run the container: `➜ backend sudo docker run -p 4000:4000 demo/simple-backend`
- view containers: `➜ backend sudo docker ps`
- stop container: `➜ backend sudo docker stop <container id>`
- start container: `➜ backend sudo docker start <container id>`

## pull & push imnages to docker hub

## setup backend w/ compose

install docker compose: https://docs.docker.com/compose/

"Volumes" are used to host data (i.e. dynamic)
"Conatiners" host static assets (i.e. the app code)

**compose:** tool that allows for managing multiple container, set backend w/ single file

create a compose file (.yaml) that creates/runs two services/containers

```bash
➜  backend2 touch docker-compose.yml
```

```
// docker-compose.yml
version: "2.0"
services:
  app:
    container_name: app
    restart: always
    build: .
    ports:
      - "4000:4000"
    links:
      - mongodb
  mongodb:
    image: mongo:latest
    container_name: mongodb
    expose:
      - "27017"
    volumes:
      - ./data/data/db
    ports: ["27017:27017"]
```

- build images (only needed for app since we specify existing/available mongo image)

```bash
➜  backend2 docker-compose build
```

- run containers (w/ mongo started first):

```bash
➜  backend2 docker-compose up -d mongo
```

- view (container) logs:
  `➜ backend2 sudo docker logs <container id>`

```
➜  backend2 sudo docker-compose up -d app
mongodb is up-to-date
Starting app ... done
➜  backend2 sudo docker ps
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                               NAMES
c8a755f3a40f        backend2_app          "docker-entrypoint.s…"   5 minutes ago       Up 4 seconds        0.0.0.0:4000->4000/tcp              app
5aa6c243a08b        mongo:latest          "docker-entrypoint.s…"   5 minutes ago       Up 5 minutes        0.0.0.0:27017->27017/tcp            mongodb
f8dbc397618b        jenkins/jenkins:lts   "/sbin/tini -- /usr/…"   23 hours ago        Up 23 hours         0.0.0.0:8080->8080/tcp, 50000/tcp   jenkins
```

## Fullstack App

create project dir with a frontend & backend folder, and docker-compose.yml file at root

```
version: "3"
services:
  app:
    container_name: app
    restart: always
    build: ./api
    ports:
      - "4000:4000"
    depends_on:
      - mongodb
  client:
    container_name: client
    restart: always
    build: ./client
    ports:
      - "3000:3000"
    links:
      - app
  mongodb:
    image: mongo:latest
    container_name: mongodb
    restart: always
    expose:
      - "27017"
    volumes:
      - ./data/data/db
    ports: ["27017:27017"]
```

build images

```bash
sudo docker-compose build
```

build containers
start services seperately

```
sudo docker-compose up -d mongodb
sudo docker-compose up -d app
sudo docker-compose up -d client
```
