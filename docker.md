# Docker
## Why it‘s used and how it works
- Docker is a tool designed to make app containers. A Docker container is a package that includes all the resources an app needs to run, once installed in an OS (e.g. code files, libraries, runtimes, DBs, etc).
- Containers make app development and deployment much simpler, since the app environment can be defined and included in the app repo. This makes the entire app ecosystem portable, removing the need to recreate it from scratch and configure it each time the app runs on a new computer.
- A container runs in the same way in any OS environment, and eliminates the worry about system dependencies, dependency versions, or any other compatibility issues.
- Containers share the services of a single operating system kernel and use fewer resources than virtual machines (which instead would require a separate OS environment for each one).
- Each container is isolated from the others and the host, because it has its own file system, its own networking, and its own isolated process tree, but can communicate through well-defined channels.
- Docker uses a client-server architecture. The Docker client talks to the Docker daemon (server), which builds and runs the Docker containers (the client and server communicate using a REST API, they can run on the same system or be remotely connected).
- The Docker client requests typically originate from the Docker CLI or from Docker Compose.
- A Docker registry stores Docker images. Docker Hub is a public registry and the default configured option (but you you can also run your own private registry). When you use the docker pull or docker run commands, the required images are pulled from your configured registry. When you use the docker push command, your image is pushed to your configured registry.

## Image
- An image is a read-only template with instructions for creating a Docker container (i.e. images become containers at runtime). Often, an image is based on another image, with some additional customization (e.g. you may build an image which is based on the ubuntu image, but installs Node.js and your app, as well as the configuration details needed to make your app run).- 
- To build an image you create a Dockerfile which defines the steps needed to create the image and run it. Each instruction in the Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only the layers that have changed are rebuilt.

## Dockerfile
- The Dockerfile is built using a range of commands, the most common ones are:
  - FROM defines the base image.
  - WORKDIR sets the working directory for all other instructions that follow in the Dockerfile. If the directory doesn’t exist, it will be created.
  - COPY copies files and directories from the host filesystem into the image. You can also create a .dockerignore file to prevent copying specified files or directories.
  - RUN runs a shell command. It’s used to install packages into the container, create folders, etc.
  - EXPOSE exposes a port to the container. It informs Docker that the container listens on a specified port at runtime.
  - ENV sets environment variables for a container, like you would have in a .env file locally.
  - CMD provides the default command for executing the resulting container.
  - LABEL adds metadata to the image.
  - VOLUME creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or containers. It is used to persist data.

```docker
# Dockerfile
FROM node:latest
WORKDIR /app
COPY package*.json .
RUN npm install
COPY . .
ENV PORT=4000
EXPOSE 4000
CMD ["npm","start"]
```

```yaml
# docker-compose.yml
version: "3.9"
services:
  db:
    image: postgres
    environment: 
      POSTGRES_PASSWORD: postgres 
      POSTGRES_USER: postgres
      POSTGRES_DB: docker-example
    volumes: 
      - ./pgdata:/var/lib/postgresql/data 
    ports:
      - '5432:5432'
  web: 
    image: dockerexample
    depends_on: 
      - db
    ports: 
      - '4000:4000'
```

## Container
- A container is a runnable instance of an image. It’s simply a process that has been isolated from all other processes on the host machine.
- A container is defined by its image as well as any configuration options you provide to it when you create it or start it. When a container is removed, any changes to its state that are not stored in persistent storage disappear.
- Compose
- It’s a tool for defining and running apps that use multiple Docker containers.
- Instructions are defined in a docker-compose.yml file to configure all the app services (e.g. you could require two services: a server and a postgresql database). For each service, you need to indicate the image and any further configuration such as depends_on, ports, environment and volumes values.
- Once a Compose file has been created, you can run the command docker compose up to start all of the containers and docker compose down to stop them.