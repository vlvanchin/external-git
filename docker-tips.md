Docker Commands:
---------------

// To pull a image 'alpine' from docker registry.  note to be logged in DockerHub site.

$ docker pull alpine

// run docker container and execute 'ls -l' command

$ docker run alpine ls -l

// view all docker containers

$ docker ps -a

// view all docker containers currently running

$ docker ps

CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS              PORTS               NAMES

55bb9c2b8530        dockersamples/static-site   "/bin/sh -c 'cd /u..."   2 minutes ago       Up 2 minutes        80/tcp, 443/tcp     vigorous_swirles


// how to execute 'echo "hello from alpine"' command

$ docker run alpine echo "hello from alpine"

// run docker container and hook up to its shell console, using -it option 'interactive terminal'

$ docker run -it alpine /bin/sh

// Run a static website in a container. this command uses -d option to run with detached mode
// run does the pull from DockerHub if the image is not locally found.

$ docker run -d dockersamples/static-site

// to get the details of running contatier

$ docker inspect <<container_id>>
ex: $ docker inspect 55bb9c2b85305b5674a37098a68f5cb7459f16ff505d332ad48b52a2a398508d

// to stop the container

$ docker stop <<container_name>>
ex: $ docker stop vigorous_swirles
$ docker stop <<container_id>>
ex: $ docker stop  55bb9c2b8530

// to start a stopped container

$ docker start <<container_name>>
ex: docker start vigorous_swirles

// to remove a stopped container

$ docker rm <<container_name>>
ex: $ docker rm vigorous_swirles
