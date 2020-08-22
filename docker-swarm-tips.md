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

[Back to Homepage](../tips-repo)
