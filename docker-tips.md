
# Docker Commands:

## Here are a few basic commands used in Docker

// To pull a image 'alpine' from docker registry.  note to be logged in DockerHub site.
```
$ docker pull alpine
```

// run docker container and execute 'ls -l' command
```
$ docker run alpine ls -l
```

// view all docker containers
```
$ docker ps -a
```

// view all docker containers currently running
```
$ docker ps
```

The above command gives the following:
```
CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS              PORTS               NAMES

55bb9c2b8530        dockersamples/static-site   "/bin/sh -c 'cd /u..."   2 minutes ago       Up 2 minutes        80/tcp, 443/tcp     vigorous_swirles
```

// how to execute 'echo "hello from alpine"' command
```
$ docker run alpine echo "hello from alpine"
```

// run docker container and hook up to its shell console, using -it option 'interactive terminal'
```
$ docker run -it alpine /bin/sh
```

## Here is how to start a static website as container

// Run a static website in a container. this command uses -d option to run with detached mode
// run does the pull from DockerHub if the image is not locally found.
```
$ docker run -d dockersamples/static-site
```

// to get the details of running contatier
```
$ docker inspect <<container_id>>
ex: $ docker inspect 55bb9c2b85305b5674a37098a68f5cb7459f16ff505d332ad48b52a2a398508d
```

// to stop the container by name
```
$ docker stop <<container_name>>
ex: $ docker stop vigorous_swirles
```

// To stop the container by container ID
```
$ docker stop <<container_id>>
ex: $ docker stop  55bb9c2b8530
```

// to start a stopped container by name
```
$ docker start <<container_name>>
ex: docker start vigorous_swirles
```

// to remove a stopped container
```
$ docker rm <<container_name>>
ex: $ docker rm vigorous_swirles
```

## How to give a name, to assign default ports and pass environment variables to a container?

// To run a named container in detached mode and passing environment variable for 'AUTHOR' and accessed through default ports.
```
$ docker run --name "static-site" -d -P -e AUTHOR="Van" dockersamples/static-site
```

// to see in which ports the container is using
```
$ docker port <<container_name>>
ex: $ docker port static-site
```

// to make a container run in specific ports: host uses 8888, continer uses 80
// goto browser and enter with localhost --> http://localhost:8888
// if container's IP is 172.17.0.3 , then in browser --> http://172.17.0.3:80
// this will display the site.
```
$ docker run --name "site-2" -d -p 8888:80 -e AUTHOR="bagsub" dockersamples/static-site
``` 

## To Remove 

// to force remove : stop and remove the container
```
$ docker rm -f <<container_name>>

ex: docker rm -f site-2
```

## To List containers

// to list all docker images found locally

```
$ docker images
```

// to list all docker images that starts with 'v' character

```
$ docker images "v*"
```

## To pull and search images

// To pull an image Ubuntu with a tag version 12.04
// if tag version not specified then 'latest' tag value is used
```
$ docker pull ubuntu:12.04
```

// to search a python container, both locally and remote
// you will have details about all the containers available
```
$ docker search python
```

## How to Create, Push and Run your own Image as a container?

Please refer to the [ link ](https://vanchin.blogspot.sg/2018/03/how-to-create-push-and-run-your-own.html)

## How to run a specific command in the docker container?

This command shows how to override the entry point defined in the image. This command would override the default entry point configured in the Dockerfile with "bin/ls" and the parameters to this command follows after the image name. 

```
$ docker run --entrypoint /bin/ls  vlvanchin/general -ls /
```


