# [Full cheat sheet](https://dockerlabs.collabnix.com/docker/cheatsheet/)
# Download images - docker pull
Downloads an image into the host

Example:
```shell
docker pull ubuntu
# Is the same as
docker pull ubuntu:latest
```

# Manage images - docker image x/y/z
Allows us to manage the images on our local system

![[Docker image commands.png]]

# Create running container - docker run

Creates running containers from images

## Commonly used flags
### -it
This will allow us to interact with the container directly
`-i` means run interactively and `-t` means to run a shell in the running container

```shell
docker run -it helloworld /bin/bash
```

### -d
Runs in detached (background) mode

```shell
docker run -d helloworld
```

### -v
Short for "Volume" - tells Docker to mount a directory or file from the host operating system to a location within the container.

```shell
docker run -v /host/os/directory:/container/directory helloworld
```

The location these files get stored is defined in the Dockerfile

### -p 

Tells Docker to bind a port on the host operating system to a port that is being exposed in the container.

```shell
docker run -p 80:80 webserver
```


### --rm
Removes the container once it finishes running.

```shell
docker run --rm helloworld
```

### --name
Names (tags) the new container

```shell
docker run --name helloworld
```


# List running containers - docker ps

## Commonly used flags
### -a
List all (including stopped) containers

```shell
docker ps -a
```

[]()# View container information - docker inspect

You can use the `docker inspect containername` command to view information about a container (including the resource limits set). If a resource limit is set to **0**, this means that no resource limits have been set.

![[Docker inspect command.png]]