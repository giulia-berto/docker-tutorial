# docker-tutorial
Docker tutorial to build an [FSL](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki) (FMRIB Software Library) container.

This simple tutorial is inspired by https://docs.docker.com/get-started/. Please refer to that resource for a more comprehensive documentation. 

### Step 1: Install docker

Important: to install and use docker you need root permission (from a terminal you can type ```sudo su``` to login as root, so you don't have to type your sudo password multiple times afterwards).

If docker isn't already installed on your machine, plese refer to these guidelines to install it: https://docs.docker.com/engine/install/.

* To check if docker is correctly installed, from a terminal run ```docker --version```.
```
$ docker --version
Docker version 19.03.13, build 4484c46d9d 
```
* To test if your installation works, from a terminal run ```docker run hello-world```.
```
$ docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.
```

### Step 2: Build your image

* Git clone this repository on your machine ```git clone git@github.com:giulia-berto/docker-tutorial.git``` and move inside the docker-tutorial directory ```cd docker-tutorial```.

* To have a working container, you need first to build the fsl image. The Dockerfile contains the instructions to do to that (in this tutorial we are building an image with fsl version 5.0). To build an fsl image named fsl:5.0, run the following command (don't forget the full stop at the end!):
```
$ docker build --tag fsl:5.0 .
```
* Check if your image was correctly built by running ```docker image ls``` and by verifying that the image fsl:5.0 is in the list.


### Step 3: Test your container

* To test if the container based on your new image runs as expected, you can run the following command:
```
$ docker run --rm -t fsl:5.0 flirt -version

FLIRT version 6.0
```
* If in your docker container you installed packages (like e.g. nibabel) using ```pip```, you can check their version using this command:
```
$ docker run -it --rm <YourDockerHubID>/RepositoryName:RepositoryTag pip show nibabel
```

### Step 4: Mount your data and run your container

You can now run your container on your data by mounting your data folder using the flag -v. In this tutorial, we check that the command fslinfo on a nifti image runs as expected. 

* The following command will mount the current working directory, in which there is a nifti file called MNI152_T1_1.25mm_brain.nii.gz, and will run the command fslinfo on it through the docker container:
```
$ docker run --rm -v `pwd`:/workdir -t fsl:5.0 fslinfo /workdir/MNI152_T1_1.25mm_brain.nii.gz
```
If the test passes successfully, you should see the following output:
```
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

### Step 5: Push your image to Docker Hub

The final step consists of sharing your image in [Docker Hub](https://hub.docker.com/) to let other users download and use it. If you don't have a Docker Hub ID, you can create one here: https://hub.docker.com/signup.

* Now it's time to create your repository. Login in with your Docker Hub ID and push the button 'Create Repository'. Type the repository name as 'fsl'.

* Name you image like ```<YourDockerHubID>/RepositoryName:RepositoryTag``` by running the following command (usually the tag corresponds to the software version):
```
$ docker tag fsl:5.0 <YourDockerHubID>/fsl:5.0
```
* Login with you Docker Hub ID also from the terminal, by typing ```docker login``` and inserting your credentials.

* Push your image to Docker Hub by running the following command:
```
$ docker push <YourDockerHubID>/fsl:5.0
```

### Step 6: Updating your container

At a certain point, you may need to update your container with a new software version. All you need to do is to replace the list of instructions in your Dockerfile (e.g. replacing 5.0 with 6.0), build the image (with a new tag), and push it to Docker Hub. In summary, after having modified the Dockerfile, you would need to run something like the following:
```
$ docker build --tag fsl:6.0 .
$ docker tag fsl:6.0 <YourDockerHubID>/fsl:6.0
$ docker push <YourDockerHubID>/fsl:6.0
```
