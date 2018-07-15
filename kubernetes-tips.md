Kubernetes Tips:
---------------

Selfhelp page to test and learn about Kubernetes.

# Install *kubectl* that CLI to access and control cluster.
- On Ubuntu

```
 $ sudo snap install kubectl --classic
```

## To test *kubectl* try the following
```
 $ kubectl version
```

the output would be as follows:

```
Client Version: version.Info{Major:"1", Minor:"11", GitVersion:"v1.11.0", GitCommit:"91e7b4fd3c980becec37ceefe", GitTreeState:"clean", BuildDate:"2018-06-27T20:17:28Z", GoVersion:"go1.10.2", Compiler:"gc", Platform:"linux/amd64"}
The connection to the server localhost:8080 was refused - did you specify the right host or port?
```

If your output is like above then it means that there is no cluster up and running. To fix this problem., install MiniKube. Please follow the next steps

# Install *MiniKube* in Ubuntu
- Please refer to the link below for more information on MiniKube
https://github.com/kubernetes/minikube

- to get the latest of the MiniKube binary
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

- to put minikube as executable
```
$ chmod +x minikube
```

- to put *minikube* in your path
```
$ sudo mv minikube /usr/local/bin/
```

# Is MiniKube installed?
- To test if minikube is install and running
```
$ minikube Version
```

* Still you would not be able to have the *kubectl version* working, as the cluster is not up yet.

# How to start Minikube cluster?
- To start a cluster through the *minikube* we need to have KVM or VM installed. But if we want to run the cluster without any vm-driver for testing purpose, we can do as follows.

```
$ minikube start --vm-driver=none
```
-- if the above command throws any permission error then try the above code in *sudo*

```
WARNING: IT IS RECOMMENDED NOT TO RUN THE NONE DRIVER ON PERSONAL WORKSTATIONS
	The 'none' driver will run an insecure kubernetes apiserver as root that may leave the host vulnerable to CSRF attacks

When using the none driver, the kubectl config and credentials generated will be root owned and will appear in the root home directory.
You will need to move the files to the appropriate location and then set the correct permissions.  An example of this is below:

	sudo mv /root/.kube $HOME/.kube # this will write over any previous configuration
	sudo chown -R $USER $HOME/.kube
	sudo chgrp -R $USER $HOME/.kube

	sudo mv /root/.minikube $HOME/.minikube # this will write over any previous configuration
	sudo chown -R $USER $HOME/.minikube
	sudo chgrp -R $USER $HOME/.minikube

This can also be done automatically by setting the env var CHANGE_MINIKUBE_NONE_USER=true
```

- Now run the following *kubectl version*, it will get the clint and server configuration.

```
Client Version: version.Info{Major:"1", Minor:"11", GitVersion:"v1.11.0", GitCommit:"91e7b4fd31fcd3dcec37ceefe", GitTreeState:"clean", BuildDate:"2018-06-27T20:17:28Z", GoVersion:"go1.10.2", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"10", GitVersion:"v1.10.0", GitCommit:"fc32d2f3698e36e9f0eaead", GitTreeState:"clean", BuildDate:"2018-03-26T16:44:10Z", GoVersion:"go1.9.3", Compiler:"gc", Platform:"linux/amd64"}
```

# How to stop the cluster?
- Run the following command
```
$ sudo minikube stop
```
