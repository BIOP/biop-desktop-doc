---
title: Run BIOP-desktop
layout: default
filename: run.md
--- 

| [Demo](/demo.md) | [Installation](/installation.md) | [Build](/build.md) | [**Run**](/run.md) | [FAQ](/faq.md) |

# Run BIOP-Desktop 

 Table of contents
- [Start BIOP-Desktop remotly](#start-biop-desktop-remotly)
    - [Kubernetes vanilla](#kubernetes-vanilla)
    - [Kubernetes RunAI](#kubernetes-runai)
    - [Slurm](#slurm)
    - [Renku](#renku)
- [Start BIOP-Desktop locally](#start-biop-desktop-locally)

- [Use BIOP-Desktop](#use-biop-desktop)



# Run BIOP-Desktop remotly

## Kubernetes vanilla

Files to use are in the [k8s](https://github.com/BIOP/BIOP-desktop/tree/main/k8s) folder on [**BIOP-desktop**](https://github.com/BIOP/BIOP-desktop) github repository

### Create pod 

#### ... using deployment

```bash
kubectl apply -f biop-desktop-deployment.yaml
```
#### ... using job
```bash
kubectl apply -f biop-desktop-job.yaml
```

## Access to jupyter
```bash
kubectl port-forward $(kubectl get pods -l app=biop-desktop -o name|head -n 1) 8888
```

or run the following command to get the pod name and specify the pod name in the following command
```bash
$ kubectl get pods 
NAME               READY   STATUS    RESTARTS   AGE
biop-desktop-0-0   1/1     Running   0          30s
$ kubectl port-forward biop-desktop-0-0 8888
```

Open [http://127.0.0.1:8888/lab](http://127.0.0.1:8888/lab) in your web browser and continue with [Use BIOP-Desktop](#use-biop-desktop)

## Cleanup
```bash
kubectl delete deployments.apps,jobs.batch -l app=biop-desktop
```

## Kubernetes RunAI

### Create pod using job
```bash
kubectl apply -f biop-desktop-runaijob.yaml
```

## Access to jupyter
```bash
kubectl port-forward $(kubectl get pods -l app=biop-desktop -o name|head -n 1) 8888
```

or run the following command to get the pod name and specify the pod name in the following command
```bash
$ kubectl get pods 
NAME               READY   STATUS    RESTARTS   AGE
biop-desktop-0-0   1/1     Running   0          30s
$ kubectl port-forward biop-desktop-0-0 8888
```

Open [http://127.0.0.1:8888/lab](http://127.0.0.1:8888/lab) in your web browser and continue with [Use BIOP-Desktop](#use-biop-desktop)

### Cleanup
```bash
kubectl delete runaijobs.run.ai -l app=biop-desktop
```

# RunAI interface   

<iframe width="640" height="360" src="https://docs.google.com/presentation/d/1420pMyae4zamCsfyuz5zT0VnYe-VlDGjydHa7PQpU4g/preview?embed?start=false&amp;loop=false&amp;delayms=60000" frameborder="0" allow="fullscreen" allowfullscreen> </iframe>


## Slurm 
(TODO)

## Renku 
(TODO)



# Start BIOP-Desktop locally

## Requirements

1.Please cf [Installation](/installation.md) 

2.a. Pull the image from [dockerhub](https://hub.docker.com/r/biop/biop-desktop) using the following command:

```
docker pull romainGuiet/biop-desktop:0.0.7
```
or 

2.b. Alternetively you can [Build](/build.md) image.


## Run 

### *(0 - Start Docker Desktop)*

### Open a command prompt and enter the following command:
```
docker run -it --rm -p 8888:8888 --gpus device=0 biop-desktop:0.0.7
```
![start terminal](/resources/local_run_00.png)

## Access to jupyter
Open [http://127.0.0.1:8888/lab](http://127.0.0.1:8888/lab) in your web browser and continue with [Use BIOP-Desktop](#use-biop-desktop)

# Use BIOP-Desktop
You arrive on JupyterLab (which is convenient to drag & drop image/file see [faq](/faq.md) for more info) 
![jupyter lab](/resources/local_JupyterLab.png)

AND **Click VNC icon** to open the Desktop

![VNC](/resources/VNC_icon.png)

### 3.You arrive on the Desktop
You access to the Desktop, you can use the software installed in the image
![desktop](/resources/local_BIOP-desktop.png)


To discover some workflows you can to have a look to [Demo](/demo.md)