Docker Commands:
---------------

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

// to stop the container
```
$ docker stop <<container_name>>
ex: $ docker stop vigorous_swirles
$ docker stop <<container_id>>
ex: $ docker stop  55bb9c2b8530
```

// to start a stopped container
```
$ docker start <<container_name>>
ex: docker start vigorous_swirles
```

// to remove a stopped container
```
$ docker rm <<container_name>>
ex: $ docker rm vigorous_swirles
```

// To run a named container in detached mode and passing environment variable for 'AUTHOR' and accessed through default ports.
```
$ docker run --name "static-site" -d -P -e AUTHOR="Susila" dockersamples/static-site
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

// to force remove : stop and remove the container
```
$ docker rm -f <<container_name>>
ex: docker rm -f site-2
```

// to list all docker images found locally
```
$ docker images
```

// to list all docker images that starts with 'v' character
```
$ docker images v*
```

// to pull an image Ubuntu with a tag version 12.04
// if tag version not specified then 'latest' tag value is used
```
$ docker pull ubuntu:12.04
```

// to search a python container, both locally and remote
// you will have details about all the containers available
```
$ docker search python
```

### creating your container image:

Steps:

1. // create an simple Maven Hello world application jar, ex: "simpleapp-0.1-SNAPSHOT.jar".
   // This jar is an executable one.
   // put this jar in an aribitary folder: docker-creation

2. // create a 'Dockerfile' that defines all the configuratios for the necessary environment for
   // the docker container.
   ```
     # base image
     FROM java:8

     # define our tmp volume
     VOLUME /tmp

     # adds our jar to the root folder
     ADD simpleapp-0.1-SNAPSHOT.jar .

     # define our CLASSPATH in environment
     ENV CLASSPATH=.:simpleapp-0.1-SNAPSHOT.jar

     # the first command to execute when the container is launched
     ENTRYPOINT ["java", "-jar", "simpleapp-0.1-SNAPSHOT.jar"]
   ```

3. // build the image 'simpleapp:latest'
```
$ docker build -t simpleapp:latest .
```

### Run the created image as a container:
```
$ docker run <<image_name>>
ex: $ docker run simpleapp:latest
```

### Push your image to DockerHub

Step 1:
// Login to DockerHub, enter the following command and provide
// the necessary credentials
```
$ docker login
```

Step 2:
// tag the image
```
$ docker tag <<image_name>> <<userid/repo_name>>
ex: $ docker tag simpleapp vlvanchin/general
```

step 3:
// Push the image
```
$ docker push <<tag_image>>
ex: $ docker push vlvanchin/general
```

### Run the push image:

// command to pull and run the image as a container
```
$ docker run <<userid/repo_name>>
ex: $ docker run vlvanchin/general
```

# Docker Swarm

### to initialize Swarm
```
$ docker swarm init
```

### how to deploy a stack of docker services
// this accepts docker-compose format file for configurations
```
$ docker stack deploy
ex: $ docker stack deploy --compose-file docker-stack.yml vote
```
// how to verify the stack has been deployed.
```
$ docker stack services vote
```
The above command's output might be as follows:

```
CONTAINER ID        IMAGE                                          COMMAND                  CREATED              STATUS              PORTS               NAMES
645ec6c9391c        dockersamples/examplevotingapp_worker:latest   "/bin/sh -c 'dotne..."   43 seconds ago       Up 34 seconds                           vote_worker.1.0cemll8gkhqbk46qikb96ueoy
c6b1915cbfd1        postgres:9.4                                   "docker-entrypoint..."   About a minute ago   Up About a minute   5432/tcp            vote_db.1.vqvw4j0c9jh8f7kxfftd685jh
e72a3e4797ef        dockersamples/visualizer:stable                "npm start"              2 minutes ago        Up About a minute   8080/tcp            vote_visualizer.1.n9v0g1gb5d2g63c84d8sdgw3q
dab5ec347f2c        redis:alpine                                   "docker-entrypoint..."   2 minutes ago        Up 2 minutes        6379/tcp            vote_redis.1.sisnubo26lxcgdsd6w7714wz5
97da6c06d251        dockersamples/examplevotingapp_vote:before     "gunicorn app:app ..."   2 minutes ago        Up 2 minutes        80/tcp              vote_vote.2.l1e5iwz3gsiypd2w1duz4xv5o
7a8a11852ac2        dockersamples/examplevotingapp_vote:before     "gunicorn app:app ..."   2 minutes ago        Up 2 minutes        80/tcp              vote_vote.1.qsklo4lpip3iscbqm0msn3t09
05d176726fb6        dockersamples/examplevotingapp_result:before   "node server.js"         3 minutes ago        Up 2 minutes        80/tcp              vote_result.1.vp04ekzbcwy997mf54jauog9r
```

### Test Run
http://localhost:5000
otherwise: http://127.0.0.1:5000

if you are trying this in AWS or Azure or any cloud, then try to port forward the request, using the following
```
$ ssh -L <<port>>:localhost:<<port>> <ssh-user>@<CLOUD_INSTANCE_IP_ADDRESS>
```

### App Customization
Change in the docker-stack.yml file to Java and .Net instead of Cats and Dogs and from before to after tags.

Redeploy the services:
  here the redeploy is same as the deployment. so we run the deploy command once again
```
  $ docker stack deploy --compose-file docker-stack.yml vote
```

### Remove the stack

```
$ docker stack rm <<stack_name>>
ex: $ docker stack rm vote
```
