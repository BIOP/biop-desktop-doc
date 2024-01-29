---
title: Installation
layout: default
filename: installation.md
--- 

| [**Installation**](/installation.md) | [Build](/build.md) | [Run](/run.md) | [FAQ](/faq.md) |

The BIOP-desktop is a docker container that can be run on a remote server or alternatively on your local machine. 
In our case we run it on a Kubernetes cluster, orchestrated by [RunAI](https://www.run.ai/).

# Remote installation

Ideally : 
- you would contact your ITs to use a remote server with a GPU.
- ITs might need to install docker and other dependencies and give you access to the server.

Then you can follow the [Run](/run.md) instructions.


# Local installation

Doing so, you will be able to run the BIOP-desktop on your local machine BUT :
- you will need to do install docker and other dependencies yourself
- you will need to figure out about drivers and GPU support yourself
- you will need to store the docker image on your local machine (which can be quite big)
- you will not have access to some software like clij/clij2/clix (as far as we know on 29.01.2024 OpenCL is not supported on WSL2) 

Don't let the few line above scare you, it is not that hard ;) and you'll get a version of the BIOP-desktop that you can use offline.

## Windows 11 & Docker Desktop

### Windows Subsystem Linux (wsl)

Follow this [wsl documentation](https://learn.microsoft.com/en-us/windows/wsl/install)

### Docker with WSL2

Follow this [docker wsl2 documentation](https://docs.docker.com/desktop/wsl/)
and this [docker-gpu documentation](https://ubuntu.com/tutorials/enabling-gpu-acceleration-on-ubuntu-on-wsl2-with-the-nvidia-cuda-platform#1-overview)

[Good reading too](https://dinhanhthi.com/docker-gpu/)

## Linux (TODO)

- Install docker

## Mac (TODO)

- Please contact us if you succesfully installed it on Mac. We will update this documentation.


# NEXT 

Please proceed with [Build](/build.md) (optionnal) OR [Run](/run.md)