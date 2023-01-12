# Devops take home assignment

## Installation
* Go through the kind installation process from their [documentation](https://kind.sigs.k8s.io/docs/user/quick-start/#installation) 

## Task

- Dockerize the `Hello World` website that's located the `src` folder.
- Deploy the `Hello World` website in an nginx reverse proxy in a pod in the kind cluster.
- Access the website from your browser.
- Document the steps on how to run the project.

## Presentation
- To present this project, push it to a github repository when you are done. 
- Setup github actions that builds and tears down the entire cluster with the pod that has the `Hello World` website. 
- Finally, invite the interviewers to the repository.


# How run this project

### The setup

Requirements:
  - ubuntu 18.04 or later

* First install requirements:
```
$ sudo apt update
$ sudo apt install curl vim git docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
* Once the environment is set I downloaded the repo
```
$ git clone https://github.com/cuerdo/devops-test.git
```

* Download and create Kind cluster

```
$ curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.17.0/kind-linux-amd64
$ chmod +x ./kind
$ sudo mv ./kind /usr/local/bin/kind
$ kind create cluster --config cluster.yml
```
* Check Cluster

```
$ kind get clusters
```

## Build and run
* Build hello-world image
```
$ docker build -t hello-world:test .
```

* Check docker images
```
$ docker images
```

* Load the image into kind cluster
```
$ kind load docker-image hello-world:latest --name=static
```

* Apply configuration files
```
$ kubectl apply -f site-deployment.yml
$ kubectl apply -f site-deployment.yml
```

* Wait until container is up
```
$ kubectl get events -w
```
## Testing

* Check availability
```
$ curl localhost:30950
``` 
