---
title: Build BIOP-destkop
layout: default
filename: build.md
--- 

| [Demo](/demo.md) | [Installation](/installation.md) | [**Build**](/build.md) | [Run](/run.md) | [FAQ](/faq.md) |

> Docker images are available on [DockerHub](https://hub.docker.com/repository/docker/romainguiet/biop-desktop/)/[GitHub](TODO), so you can simply pull and run them. 
>
> Nevetherless, if you want to build the images yourself, you can follow the instructions below.


# Build MAIN image

```
docker build -f Dockerfile-ms -t biop-desktop:0.0.7 .
```

# Build sub-block

The origin image is [nvidia/pytorch](https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel-23-07.html ), based on Ubuntu 22.04 including :
- Python 3.10
- NVIDIA CUDA® 12.1.1
- Pytorch 2.1.2

In the [DockerFile-base](/docker/DockerFile-base) you will notice the following line :
```dockerfile
FROM nvcr.io/nvidia/pytorch:23.07-py3
```

When building the main image via [DockerFile-ms](/docker/DockerFile-ms) we make use of multi-stage build, i.e. using smaller image containing a software. 
The rational for this is to "simplify" the build when you want to change a single "program" one doesn't need to build everything from scratch but rather create a new sub-block and update the main.

```
├── nvcr.io/nvidia/pytorch /
│   └── biop-vnc-base/
│       ├── biop-qupath
│       ├── biop-ilastik
│       ├── biop-cellpose
│       ├── biop-devbio
│       ├── biop-samapi
│       ├── biop-empanada
│       ├── biop-desktop (the main image)
|       └── biop-fiji
└── nvcr.io/nvidia/tensorflow
    └── biop-stardist
```
graph above made with [this tool](https://tree.nathanfriend.io/)

More details about the version of each component can be found in the spreadsheet below :
<iframe width="350" height="550"  src="https://docs.google.com/spreadsheets/d/e/2PACX-1vRwd66lBsfJX8kvYwbSxRJbApiAdD-KDfO5PeGHjstlKjE2XsiCf2Ene81AbJYVzHZ73qN3-_m2VtfI/pubhtml?widget=true&amp;headers=false"></iframe>

## How does it work ?

Looking at the [DockerFile-ms](/docker/DockerFile-ms)  you will notice some lines like :

```dockerfile
ARG QUPATH_VERSION=v0.4.4
FROM biop-qupath:${QUPATH_VERSION} as qupath-image
...
COPY --from=qupath-image /opt/QuPath /opt/QuPath
```

It's literally doing what you think it is doing : We copy the entire QuPath folder from one image to the other!


## Update a sub-block and build main image 

The main image is built using multi-stage build, i.e. using smaller image containing a software. 

The main image and the sub-blocks are all based on the [Dockerfile-base](/docker/Dockerfile-base) file. 
Exceptions being for Stardist (based on tensorflow).

| Dockerfile | Docker Image | Origin | Notes | 
| :--- | :---  | :---  | :---  |
| Dockerfile-ms | biop-vnc-ms | biop-vnc-base:0.0.3 | Contains everything , using multi-stage to build only necessary  | 
| Dockerfile-base |  biop-vnc-base:0.0.1 | nvcr.io/nvidia/pytorch:23.07-py3 | Base image with pytorch, noVNC dekstop, conda installed |
| qupath/Dockerfile-qupath | biop-qupath:v0.4.4 | biop-vnc-base:0.0.1 |
| ilastik/Dockerfile-ilastik | biop-ilastik:1.4.0-gpu | biop-vnc-base:0.0.1 |
| fiji/Dockerfile-fiji | biop-fiji:20230920 | biop-vnc-base:0.0.2 |
| cellpose/Dockerfile-cellpose | biop-cellpose:2.2.2 | biop-vnc-base:0.0.1 |
| devbio/Dockerfile-devbio | biop-devbio:0.10.1 | biop-vnc-base:0.0.1 
| samapi/Dockerfile-samapi | biop-samapi:0.3.0 | biop-vnc-base:0.0.1 |
| empanada/Dockerfile-empanada | biop-samapi:0.2.3 | biop-vnc-base:0.0.1 |
| stardist/Dockerfile-stardist | biop-stardist: | nvcr.io/nvidia/tensorflow:23.07-tf2-py3 |
| abba/Dockerfile-abba | biop-abba:0.0.2 | biop-vnc-base:0.0.1 |


Whenever you want to update a "sub-block" (QuPath, ilastik, Fiji ... ) :
- first you build the **desired block**
- second you build the **main image**


## Advantage of multi-stage build

The main advantage of multi-stage build is that you can build only the sub-block you want to update, and then build the main image saving some time compare to building everything from scratch each time you want to update a single software.

In the table below, you can compare the time needed to build a sub-block image, or the single step of conda create & install and finally the "COPY/PASTE" from one image to the other.

| Dockefile |	TOTAL BUILD	(sec) | conda install (sec) |	multistage - COPY (sec) |
| ----- | ----- | -----| ----- |
| Dockerfile-cellpose |	362.9	|295.6	| 63.2 |
| Dockerfile-devbio |	283.9|	242.8|	54.2 |
| Dockerfile-samapi	| 560.4	| 508.2	| 155.9 | 


# Build sub-blocks

The base should change as little as possible 🤞 

```
docker build -f Dockerfile-base  -t biop-vnc-base:0.0.3 . --no-cache
```

## QuPath and ilastik 

Whenever you want to update a "sub-block" QuPath or ilastik, you can build it with the following command :

```
docker build -f QuPath/Dockerfile-qupath -t biop-qupath:v0.4.4 . --no-cache --build-arg="BASE_IMAGE=0.0.1" --build-arg="QP_VERSION='v0.4.4'"
```

```
docker build -f ilastik/Dockerfile-ilastik -t biop-ilastik:1.4.0-gpu . --no-cache --build-arg="BASE_IMAGE=0.0.1" --build-arg="ILASTIK_VERSION=1.4.0-gpu"
```

The `--build-arg` are used to pass arguments to the Dockerfile, in this case the base image and the version of the software to install.
They are optionnal, if not provided the default values are used. The default value is defined in the Dockerfile, for example :

```dockerfile
ARG QP_VERSION='v0.4.4'
```
This is useful when you want to test the build of a new version of a software, without having to change the Dockerfile.
(Nevertheless after the test you should update the Dockerfile with the new version and commit it to the repository.)


## Fiji

Whenever you want to update the sub-block Fiji, you can build it with the following command, replacing YYYYMMDD with the date of the build :

```
docker build -f fiji/Dockerfile-fiji -t biop-fiji:YYYYMMDD . --no-cache --build-arg="BASE_IMAGE=0.0.2" 
```

Because we rely on update site, **the build is not reproducible**, hence the tag is the date of the build!

## Cellpose, devbio, samapi, empanada ...

Here we'll build the sub-blocks cellpose (devbio, samapi, empanada ...)  using a yml file and a conda command in the dockerfile.
To simplify the maintenance we create an independent conda env per software, and we use the version number of the software as tag for the image.

In order to update the sub-block, you need to :
- first **update the yml file**
- second **build the image**, using the following command :

```
docker build -f cellpose/Dockerfile-cellpose -t biop-cellpose:2.2.2 . --no-cache --build-arg="BASE_IMAGE=0.0.3"
```

```
docker build -f devbio/Dockerfile-devbio -t biop-devbio:0.10.1 . --no-cache --build-arg="BASE_IMAGE=0.0.3"
```

```
docker build -f samapi/Dockerfile-samapi -t biop-samapi:0.3.0 . --no-cache --build-arg="BASE_IMAGE=0.0.3"
```

```
docker build -f empanada/Dockerfile-empanada -t biop-empanada:0.2.3 . --no-cache --build-arg="BASE_IMAGE=0.0.3"
```

```
docker build -f stardist/Dockerfile-stardist -t biop-stardist:0.8.5 . --no-cache --build-arg="BASE_IMAGE=0.0.3"
```

(here again --build-arg is optionnal)


# Build the main image 

By specifying the version of the sub-blocks (needs to be built in advance, see above), we can build the main image with the following command (--build-arg(s) are optionnal) :

```
docker build -f Dockerfile-ms -t biop-desktop:0.0.8 . --no-cache
```


```
docker build -f Dockerfile-ms -t biop-desktop:0.0.8 . --no-cache --build-arg="BASE_IMAGE=0.0.1" --build-arg="QUPATH_VERSION=v0.4.4" --build-arg="ILASTIK_VERSION=1.4.0-gpu" --build-arg="FIJI_VERSION=20230920" --build-arg="CELLPOSE_VERSION=2.2.2" --build-arg="SAMAPI_VERSION=0.3.0" --build-arg="EM_VERSION=0.2.3"
```

# NOTES

Docker image is big because of :

- models pre-download
	cellpose (all models ~350 Mo)
	samapi (huge et large  > 5Go)

	if we don't download, image will get smaller
	BUT users will have to download models each time (possibility of hosting server being done at that time)

- multiple conda-env (cellpose, samapi , ~5Go each)
	
	- easier to maintain multiple envs than one env containing everything (if ever possible to create)



# NEXT 

Please proceed with [Run](/run.md) 
