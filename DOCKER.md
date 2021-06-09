# Useful docker commands

This markdown document contains some useful and commonly used docker commands.

## Dockerhub

Logging into docker hub:

```shell
docker login docker.io

# if you want to use it scripts
cat ~/my_password.txt | docker login --username <username> --password-stdin
```

Pushing to docker hub:

```shell
# Tag the image
docker tag <image_id> <username>/<reponame>:tag

# push to docker hub
docker push <username>/<reponame>

# if you get the following error: denied: requested access to the resource is denied
docker login docker.io
```

Pulling from docker hub:

```shell
docker pull <username>/<image_name>:tag
```

## Managing containers

Listing containers:

```shell
# ps = list running containers
# -a list all containers
docker ps -a
```

Starting a container:

```shell
# -d = detached (it doesn't write its output to the terminal)
# -P = expose ports to random ports
# --name = name the container
# --rm = remove the container once it exits
docker run --rm -d -P --name <container_name> <image_name>

# -p = connect exposed port from the dockerfile to port in the host
docker run -p <host_port>:<docker_container_port> <image_name>
```

Stopping a container:

```shell
docker stop <container_id>
```

## Managing images

Listing all images:

```shell
docker images
```

Deleting an image:

```shell
docker image rm <image_id>
```

Building an image from a dockerfile:

```shell
# -t = tag
# . = path to the dockerfile (. specifies current working directory)
docker build -t <image_name> .
```

## "Debugging"

A really practical way of debugging dockerfiles is accesing the running container's file system.
If it has a defined entrypoint, then this needs to be overwritten. This can be achieved with the --entrypoint option: 

```shell
# if the image has a defined entrypoint
# run in interactive mode
docker run -it --entrypoint sh <image_tag>
```

If the image does not have a defined entrypoint (the last command is not ENTRYPOINT):

```shell
# -it = interactive
docker run -it <image_id> sh
```

Alternatively, you can "ssh" into a running container.

```shell
# get container's name
docker ps

# exec = execute command
# -it = interactive mode
# sh = shell. If this gives an error, then try it with /bin/bash
docker exec -it <container_name> sh
```

## General

Get docker version:

```shell
docker version
```

Delete unused data:

```shell
# Removes all dangling images and containers
docker system prune

# -a = remove all unused images, not just dangling ones
# -f = force, doesn't prompt for confirmation
docker system prune -f -a
```