+++
title = "docker cheatsheet"
date = 2023-09-03
[taxonomies]
tags = ['computer science', 'cheatsheet']
+++

👋 Hello

**This is the docker cheatsheet**

### General info

```
docker --version
docker info
```

### Containers

```
docker container ls
docker container ls --all     # see stopped containers also
docker container ls --all -q  # see stopped containers; get the id only
docker container ls -aq       # see stopped containers; get the id only
```

### Images

```
docker images           # see what is available
docker image ls         # see what is available
docker rmi <image id>   # remove an image
```

### Running containers

```
docker ps          # see what is running
docker ps -a       # see everything, even stopped containers
docker ps -a -q    # get just the container IDs for all jobs
docker create      # "stage" a container (then `start` it)
docker stop        # stop a container
docker kill        # kill a container
docker start       # start a container
docker restart     # restart a container
docker rm          # remove the container (can't `restart` it then)
docker stop $(docker ps -q)     # stop all containers
docker rm $(docker ps -a -q)    # remove all stopped containers
```

### Connect to a service in a container, e.g. **TensorFlow**

First we map 8888 (Jupyter notebook) on the "inside" to 5000 on the "outside"
and run the image containing TensorFlow:

```
docker run -it -v "$PWD":/mnist -p 5000:8888 b.gcr.io/tensorflow/tensorflow:latest-devel
```

(This also maps the current directory to a mount in the docker container.)
Then, we launch ***ipython notebook*** inside the image. Next, we get the correct
host IP address with:

```
docker-machine ls
```

This will provide a URL, e.g. ***tcp://192.168.XYZ.XYZ:ABCD***. Point a browser to
***192.168.XYZ.XYZ:5000*** and we will see the notebook.

### Pushing to DockerHub

e.g., the ***iqsharp*** container:

```
docker login
docker tag iqsharp gnperdue/iqsharp
docker push gnperdue/iqsharp
```

### Pulling from DockerHub

```
docker pull gnperdue/kubia
```