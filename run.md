---
title: Run BIOP-Desktop
layout: default
filename: run.md
--- 

# Run BIOP-Desktop locally

## Requirements

1.Please cf [Installation](/installation.md) 
2.a.Please cf [Build](/build.md) 

or 

2.b.Pull the image from [dockerhub](https://hub.docker.com/r/biop/biop-desktop) using the following command:

```
docker pull romainGuiet/biop-desktop:0.0.7
```

## Run 

### *(0 - Start Docker Desktop)*

### 1.Open a command prompt and type:

![start terminal](/resources/local_run_00.png)

```
docker run -it --rm -p 8888:8888 --gpus device=0 biop-desktop:0.0.7
```

![start jupyter lab](/resources/local_run_01.png)

### 2.a. Ctrl+click on the link in the command prompt 

OR

### 2.b. Open a browser and go to [http://127.0.0.1:8888/lab/](http://127.0.0.1:8888/lab/) to arrive on JupyterLab (convenient to drag & drop images/files)
![jupyter lab](/resources/local_JupyterLab.png)
AND 
**Click VNC icon**
![VNC](/resources/VNC_icon.png)

### 2.c. Open a browser and go to [http://127.0.0.1:8888/vnc/](http://127.0.0.1:8888/vnc/) for direct access to Desktop

### 3.You arrive on the Desktop
![desktop](/resources/local_BIOP-desktop.png)

#### Binding local folder/hardrive

You can mount a folder from your computer to the docker container using the following command:

```
docker run -it --rm -p 8888:8888 --gpus device=0 --mount src=where/on/your/computer,target=where/in/the/docker,type=bind biop-desktop:0.0.7
```

# Run BIOP-Desktop remotly

## Kubernetes

### General
TODO

### RunAI
TODO

## Slurm

TODO

## Renku

TODO



| | [Build](/build.md) | [Run](/run.md) |