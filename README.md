# minikube-spring-mongodb

# Step by Step Installation Guide

``` 
Install Docker Desktop on Windows 10
```
```
https://docs.docker.com/docker-for-windows/install/

In the Windows Desktop the Setting should look like this.

```

![alt text](https://github.com/beethovenX/minikube-spring-mongodb/blob/master/installation-guide/docker_settings.JPG?raw=true)
```
After selecting this stuff click apply and restart
```
``` 
Here is how you should add the DOCKER_HOST environment variable to the System variables.
```
![alt_text](https://github.com/beethovenX/minikube-spring-mongodb/blob/master/installation-guide/System_Variables.JPG?raw=true)


# Set up the windows environment to work with WSL ( Windows Subsytem for Linux).

```
Follow the steps in the following URL
https://docs.microsoft.com/en-us/windows/wsl/install-win10
```

```
Install the choco Package Manager to use with the Windows Power Shell.
https://chocolatey.org/
```

``` 
Note: Go the the Program menu select Power Shell and open it as an administrator.
We will be running all the minikube, docker and kubectl commands from the Windows Power Shell
```

# Install Kubernetes

```
Follow the Instructions given on this page. You can use either by downloading the .exe file or with the help of choco package manager.
https://kubernetes.io/docs/tasks/tools/install-kubectl/
```

# Install the minikube and configure it with your Kubectl

``` 
Follow the instructions on this page to install the minikube.
https://minikube.sigs.k8s.io/docs/start/
```



