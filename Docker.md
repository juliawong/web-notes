* http://prakhar.me/docker-curriculum/
* https://docs.docker.com/engine/getstarted

# What

* Deploy applications in containers that act like sandboxes
* More efficient than VMs

## Containers

```
docker run hello-world
```

* `run` is a subcommand that creates and runs the container
* `hello-world` is the image to load into the container
* Running instance of an image
* New one created each time

## Images

* Filesystem and parameters to use at runtime
* No state
* Blueprints that form the basis of containers

Types

* Base have no parent e.g. ubuntu, busybox, etc.
* Child build on base images and add additional functionality e.g. whalesay-fortune

Versions
* onbuild includes helpers to automate parts of the app

# Dockerfile

* List of commands Docker client calls while creating an image

```docker
# base image
FROM python:3-onbuild

# specify the port number the container should expose
EXPOSE 5000

# run the application
CMD ["python", "./app.py"]
```

```docker
# base image
FROM docker/whalesay:latest

# get fortunes
RUN apt-get -y update && apt-get install -y fortunes

# run application
CMD /usr/games/fortune -a | cowsay
```


# Commands

`docker images` show all images

`docker ps` show containers currently running
* `-a` show all containers previously run
* `-it` interactive tty

`docker run docker/whalesay cowsay boo` runs an image and provides parameters

`docker build -t docker-whale .` builds a new image from `pwd` and names it `docker-whale`

`docker tag 7d9495d03763 username/docker-whale:latest` associate with account

`docker push username/docker-whale` add to Docker Hub
