# docker-tutorial
Docker tutorial to build an [FSL](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki) container.

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

* Git clone this repository on your machine ```git clone git@github.com:giulia-berto/docker-tutorial.git``` and move inside the docker-tutorial directory ```cd docker-tutorial```.

* The Dockerfile contains the instructions to create the container. To have a working container, you need first to build the fsl image by running the following command (don't forget the full stop at the end):
```
docker build --tag fsl:5.0 .
```
* (Finally, you can start a container based on your new image. To test if it runs as expected, you can run the following command (be sure to replcae ```/absolute/path/to/directory``` with your actual absolute path):
```
docker run --rm -v /absolute/path/to/directory/docker-tutorial:/workdir -t fsl:5.0 /workdir/test
```
  If the test passed successfully, you should see the following output:
```
This is a test.
/usr/share/fsl/5.0
FLIRT version 6.0
data_type      INT16
dim1           145
dim2           174
dim3           145
dim4           1
datatype       4
pixdim1        1.250000
pixdim2        1.250000
pixdim3        1.250000
pixdim4        1.000000
cal_max        0.0000
cal_min        0.0000
file_type      NIFTI-1+
```
)
