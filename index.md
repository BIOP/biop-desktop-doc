---
title : Welcome
layout: default
filename: index.md
---

| [Installation](/installation.md) | [Build](/build.md) | [Run](/run.md) |

# Acknowledgements 

This whole project was possible thanks to the previous work of the [renku team](https://renkulab.io/) ([renku-desktop](https://renkulab.io/projects/learn-renku/renku-desktop)) and the support of the [RCP](https://www.epfl.ch/research/facilities/rcp/) and [SV IT](https://www.epfl.ch/schools/sv/it/) teams, [EPFL](https://www.epfl.ch/en/).


# Introduction

The BIOP-desktop is a **`Versioned Computer`** with [software]() pre-installed and pre-configured so you can focus on your analysis (and not on the installation).

![desktop-screeshot](/resources/BIOP-desktop.png)

The **BIOP-desktop** is :

| Users Point of View | IT & Dev. Point of View |
|---|---|
| a **`Computer`** with "everything" installed and running! | a **`Docker`** image that you can simply pull and run |



## What is a Versioned Computer?

By **`Versioned Computer`**, we mean a computer in which every software is fixed, making it possible to reproduce the same environment at any time.

Making use of the [Docker images](https://docs.docker.com/manuals/), we can create a **`Versioned Computer`** that is reproducible, shareable, and open.
We make use of [multi-stage build](https://docs.docker.com/build/building/multi-stage/) to ease building and versionning. Indeed we can build a new image, changing a single component and keeping the rest of the image unchanged, if needed.

## What is a Versioned Computer for?

A **`Versioned Computer`** is useful for:
- **Focusing on your analysis**: you don't have to worry about installing and configuring software.
- **Reproducibility**: you can reproduce your analysis at any time, even years later.
- **Collaboration**: you can share your analysis with your collaborators, and they can reproduce it.
- **Teaching**: you can share your analysis with your students, and they can reproduce it.
- **Publication**: you can share your analysis with the reviewers, and they can reproduce it.
- **Open Science**: you can share your analysis with the world, and they can reproduce it.

# BIOP-desktop installed software

| Software | Description | Notes | 
| --- | --- |
| [Fiji](https://fiji.sc/) | a “batteries-included” ImageJ  | update sites : clij, stardist, ptbiop , ilastik … |
| [ilastik (GPU)](https://www.ilastik.org/) | interactive learning and segmentation toolkit | GPU version|
| [QuPath](https://qupath.github.io/) | Digital Pathology | with extensions : cellpose, samapi extension , ABBA ... |
| [cellprofiler](https://cellprofiler.org/) | |
| [devbio-napari](https://github.com/haesleinhuepf/devbio-napari) | The Fijiest way to do image analysis in Python | 
| [EMPanADA](https://empanada.readthedocs.io/en/latest/)| DNN to segment mitochondria in EM images | 
| [stardist](https://github.com/stardist/stardist) | |
| [ABBA](https://biop.github.io/ijp-imagetoatlas/) | including : elastix, transformix, DeepSlice, ... | | 
| [inkscape](https://inkscape.org/) |  Vectoriel drawing (and more!) | 


