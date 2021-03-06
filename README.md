# Useful commands for docker, for those who forget easily

Such as me :)

## Basic commands
```shell

# Finding containers
docker container ls -a # show all containers
docker container ls -a | grep <name> # show all containers and pipe to grep to display what you want
 
# Finding images
docker image ls
 
# Removing containers
docker container rm <container> # remove container with id, you can actually use only the initial charaters for this (docker conatainer rm 3d for 3d4bab29dd67)
docker container rm --force <container> # force remove. UNSAFE!
docker container prune # remove all stopped containers
docker image prune # remove dangling images
docker system prune # just nuke everything

# Removing images
docker image rm <image>

# Download
docker image pull <name>:<tag> # download an image without running it from docker registry, if tag is omitted, defaults to latest release

# Run
docker container run <container> <args> # download and run a container, use -d flag before name to detach, args used to execute commands
docker container exec <container> # executes a command inside the container 

# Stop
docker container stop <name> # stop a container of a given name

# Tag
docker tag ubuntu:18.04 <name>:<tag> # create a custom tag for ubuntu 18.04 and renames the image

# Flags
-i (interactive)
-t (tty)
-d (detached)

# Docker build
docker build . -t hello-docker # builds a docker image named "hello-docker" from current directory Dockerfile

# Volume
docker run -v "$(pwd)/text.log:/usr/src/app/text.log" devopsdockeruh/simple-web-service # container input in text.log, will also show in text.log in our computer

# Port mapping
 docker run -p <host-port>:<container-port> <image> # run a container from image and map ports
```
### From DevOps with Docker 2021 course material
| command                             | explain                                 | shorthand      |
|-------------------------------------|-----------------------------------------|----------------|
| docker image ls                     | Lists all images                        | docker images  |
| docker image rm \<image\>           | Removes an image                        | docker rmi     |
| docker image pull \<image\>         | Pulls image from a docker registry      | docker pull    |
| docker container ls -a              | Lists all containers                    | docker ps -a   |
| docker container run \<image\>      | Runs a container from an image          | docker run     |
| docker container rm \<container\>   | Removes a container                     | docker rm      |
| docker container stop \<container\> | Stops a container                       | docker stop    |
| docker container exec \<container\> | Executes a command inside the container | docker exec    |

## Ubuntu and other linux distros

```shell
 docker run -it ubuntu # run ubuntu with terminal and input enabled
 docker run -d -it --name looper ubuntu sh -c 'while true; do date; sleep 1; done' # run ubuntu container named "looper" with a shell script
 docker logs -f looper # show logs from that container
 docker pause looper # pause looper
 docker unpause looper # unpause looper
 docker attach looper # attach looper to your terminal
 docker attach --no-stdin looper # attach looper to your terminal, but without std in
 docker exec -it looper bash # enter looper container with terminal and input enabled
 
 # equivalent to running docker rm --force looper
 docker kill looper 
 docker rm looper 
 
 docker run -d --rm -it --name looper-it ubuntu sh -c 'while true; do date; sleep 1; done' # --rm removes looper after it exits
 
 docker cp path/to/file.extension <name>:/path/to/destination # copy a file inside dockerized linux
 docker diff <name> # what has changed inside container linux
 docker commit <name> <image> # commit changes to a new image, maybe not that useful because of dockerfile
```
