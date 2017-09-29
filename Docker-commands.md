List all Docker Images

    docker images -a

List All Running Docker Containers

    docker ps

List All Docker Containers

   docker ps -a

Start a Docker Container

    docker start <container name>

Stop a Docker Container

    docker stop <container name>

Kill All Running Containers

    docker kill $(docker ps -q)

View the logs of a Running Docker Container

    docker logs <container name>

Delete All Stopped Docker Containers

   Use -f option to nuke the running containers too.

    docker rm $(docker ps -a -q)

Remove a Docker Image

    docker rmi <image name>

Delete All Docker Images

    docker rmi $(docker images -q)

Delete All Untagged (dangling) Docker Images

    docker rmi $(docker images -q -f dangling=true)

Delete All Images

    docker rmi $(docker images -q)

Remove Dangling Volumes

    docker volume rm -f $(docker volume ls -f dangling=true -q)

SSH Into a Running Docker Container


     sudo docker exec -it <container name> bash

Use Docker Compose to Build Containers
Run from directory of your docker-compose.yml file.


    docker-compose build

Use Docker Compose to Start a Group of Containers
Use this command from directory of your docker-compose.yml file.


    docker-compose up -d

This will tell Docker to fetch the latest version of the container from the repo, and not use the local cache.


    docker-compose up -d --force-recreate

This can be problematic if you’re doing CI builds with Jenkins and pushing Docker images to another host, or using for CI testing. I was deploying a Spring Boot Web Application from Jekins, and found the docker container was not getting refreshed with the latest Spring Boot artifact.


     #stop docker containers, and rebuild
     docker-compose stop -t 1
     docker-compose rm -f
     docker-compose pull
     docker-compose build
     docker-compose up -d

    #stop docker containers, and rebuild
    docker-compose stop -t 1
    docker-compose rm -f
    docker-compose pull
    docker-compose build
    docker-compose up -d

Follow the Logs of Running Docker Containers With Docker Compose

    docker-compose logs -f

Save a Running Docker Container as an Image


    docker commit <image name> <name for image>

Follow the logs of one container running under Docker Compose


     docker-compose logs pump <name>
