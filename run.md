Run BIOP-Dekstop

# Locally

## Requirements

### Windows 11 & Docker Desktop

#### Run BIOP-Desktop

Open a command prompt and type:

```
docker run -it --rm -p 8888:8888 --gpus device=0 biop-desktop:0.0.7
```

#### Binding local folder/hardrive

You can mount a folder from your computer to the docker container using the following command:

```
docker run -it --rm -p 8888:8888 --gpus device=0 --mount src=where/on/your/computer,target=where/in/the/docker,type=bind biop-desktop:0.0.7
```

# Remote

## Kubernetes

### General
TODO

### RunAI
TODO

## Slurm

TODO

## Renku

TODO



 | [Home](/index.md)| [Installation](/installation.md) | [Build](/build.md) | [Run](/run.md) |
 |---|---|---|---|