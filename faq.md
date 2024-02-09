---
title: Frequently Asked Questions of BIOP-destkop
layout: default
filename: faq.md
--- 

| [Demo](/demo.md) | [Installation](/installation.md) | [Build](/build.md) | [Run](/run.md) | [**FAQ**](/faq.md) |

# Frequently Asked Questions

## How to update the BIOP-desktop ?

End-user can't update the BIOP-desktop, you need to pull the new updated image and run it.

## How to update a software ?

You can't update a software, you need to build a new image with the updated software.

## How to add a software ?

You need to build a new image with the new software, please cf [Build](/build.md), open an issue or a pull request.

## How to exchange data to BIOP-desktop?

Multiple options are available depending of the data size and of your hardware (local computer or remote).

### OMERO

BIOP-desktop is ideally suited if your data are hosted on an OMERO server

### ZIP

When running the BIOP-desktop (locally or remotely), you can **drag and drop** file from your computer to the Jupyter Lab interface. 
The file will be accessible from the Desktop, in your "home" folder.

> NOTE : You can NOT drag and drop **folder**, but you can :
> - zip the folder
> - drag & drop the zip!
> - unzip from the BIOP-desktop

In the Jupyter Lab interface, you can get into a folder, right-click to save the folder as a zip.

### Mount folder (locally)

When running the BIOP-desktop locally, you can mount a folder from your computer to the BIOP-desktop when you START the BIOP-desktop.

```docker run -it --rm -p 8888:8888 --gpus device=0 --mount src=where/on/your/computer,target=where/in/the/docker,type=bind biop-desktop:0.0.7```

### Mount folder (remotely)

When running the BIOP-desktop remotely, you can mount an S3 storage to the BIOP-desktop when you START the BIOP-desktop. 
Please get in touch with your IT.


## How to skip jupyter lab interface and arrive directly on the BIOP-desktop ?

Open a browser and go to [http://127.0.0.1:8888/vnc/](http://127.0.0.1:8888/vnc/)! 

