# docker-tutorial
Docker tutorial to build an FSL container.

This simple tutorial is inspired by https://docs.docker.com/get-started/. Please refer to that resource for a more comprehensive documentation.

### Step 1: Install docker

If docker isn't already installed on your machine, plese refer to these guidelines to install it: https://docs.docker.com/engine/install/.

To check if docker is correctly installed, from a terminal run ```docker --version``` (you need root permission, type ```sudo su``` to login as root).
```
$ docker --version
Docker version 19.03.13, build 4484c46d9d 
```
To test if your installation works, from a terminal run ```docker run hello-world```.
```
$docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.
```

### Step 2: Build and run your image

- Git clone this repository on your machine ```git clone git@github.com:giulia-berto/docker-tutorial.git``` and move inside the docker-tutorial directory ```cd docker-tutorial```.

- The Dockerfile contains the instructions to create the container.
