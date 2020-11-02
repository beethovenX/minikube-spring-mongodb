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

## Project Set UP

```
1. Make sure the minikube is running and it is working well with the Kubectl.
2. You need to signin/signup to https://hub.docker.com/ because we will pushing and pulling docker images to the hub while setting up the project.
```

# Build the jar of the API service.

```
1. Go to the Directory where you have cloned the repository in Windows Power shell or Git Bash ( You will have to install Git bash for windows.) and run the following
   commands
   
   $ cd api-service
   $ mvn package -DskipTests=True

This will create a jar file that we will be using in our Dockerfile.   
```

# Create the Docker images of the application and push to the Docker Hub

```
Make sure you have logged in to the docker hub as well from the cli.

  $ cd api-service
  $ docker build -t mozartx/api-service .
  $ docker push mozartx/api-service

You will have to create the repo on the docker hub to push your image for example in my case my username is mozartx and my repo name is api-service.
```

# Settings for Mongo
# Create the Persistant Volume for Mongo

```
  $ cd manifests
  $ kubectl create -f mongo-pv.yml
  $ kubectl get pv

Make sure you run these commands from root directory of the project.
```

# Create Persistant Volume  Claim

```
  $ cd manifests
  $ kubectl create -f mongo-pvc.yml
  $ kubectl get pvc
```

# Create MongoDb Controller

```
  $ cd manifests
  $ kubectl create -f mongo-controller.yml
```

# Create MongoDB Service

```
  $ cd manifests
  $ kubectl create -f mongo-service.yml
```

# Create API Deployment
```
  $ cd manifests
  $ kubectl create -f api-deploy.yml

You can check the deployment by using the following command
  
  $ kubectl get deployments
  $ kubectl get pods
  
```

# Create API Service

```
  $ cd manifests
  $ kubectl create -f api-service.yml
  
You can check the deloyed service with following commands

  $ kubectl get services
  $ kubectl describe svc <service-name>
  
Since this we have deployed this application with the node port (Check the api-service.yml file.)
you can get the node port using the above command.

So if everything is deployed correctly then you will be able to hit the exposed endpoints with your the following command.

  $ minikube service <service-name>

This will open the url in the browser, You can grab that url and use this URL along with the endpoints to hit the deployed api.

```

# Curls for the API

# Curl to create a Student ( Write into Mongo DB)

```
curl --location --request POST 'http://127.0.0.1:57006/student' \
--header 'Content-Type: application/json' \
-d '{
	"id": "1",
	"name": "Aman Kalotra",
	"description": "Programmer",
	"courses": [{
		"id": "1",
		"name": "Minikube on local",
		"description": "Kubenetes",
		"steps": [1]
	}]
}'
```

# Curl to get all the students ( Read from Mongo DB.)
```
curl --location --request GET 'http://127.0.0.1:57006/students' \
--data-raw ''
```

# Curl to get the Student by Id

```
curl --location --request GET 'http://127.0.0.1:57006/students/1' \
--data-raw ''
```

# Curl to get the Student by Name

```
curl --location --request GET 'http://127.0.0.1:57006/students/page?name=Aman%20Kalotra' \
--data-raw ''
```

# Some debugging commands

``` 
Use following commands to check the logs of the pods

   $ kubectl get pods
   $ kubectl logs <pod name>
```







  


  
   



