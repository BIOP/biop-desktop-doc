---
title : Welcome to BIOP-desktop
layout: default
filename: index.md
---

| [Demo](/demo.md) | [Installation](/installation.md) | [Build](/build.md) | [Run](/run.md) | [FAQ](/faq.md) |

# Acknowledgements 

This whole project was possible thanks to the previous work of the [renku team](https://renkulab.io/) ([renku-desktop](https://renkulab.io/projects/learn-renku/renku-desktop)) and the support of the [RCP](https://www.epfl.ch/research/facilities/rcp/) and [SV IT](https://www.epfl.ch/schools/sv/it/) teams, [EPFL](https://www.epfl.ch/en/).


# Introduction

The BIOP-desktop is a **`Versioned Computer`** with [software](#BIOP-desktop-installed-software) pre-installed and pre-configured so you can focus on your analysis (and not on the installation).

![desktop-screeshot](/resources/BIOP-desktop_Shot.png)

The **BIOP-desktop** is a [Docker](https://www.docker.com/) image that you can simply pull and run (and optionnaly build yourself)

![BIOP-desktop_Fresk](/resources/BIOP-desktop_Fresk.png)
( [*enlarge image*](https://github.com/BIOP/biop-desktop-doc/blob/main/resources/BIOP-desktop_Fresk.png) )

The **BIOP-desktop** is :

|  *Developper* Point of View | *IT* Point of View |     *Users* Point of View |
|---|---|---|
| a **`Docker`** image that you can [build](/build.md) using multi-stage | a **`Docker`** image that you can simply pull and [run](/run.md) |  a **`Computer`** with "everything" installed and running! |


## What is a Versioned Computer?

By **`Versioned Computer`**, we mean a computer in which every software is set, making it possible to reproduce the same environment at any time.

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
| --- | --- |--- |
| [ABBA](https://biop.github.io/ijp-imagetoatlas/) | Aligning Big Brains & Atlases| including : [elastix](https://elastix.lumc.nl/) & transformix, [DeepSlice](https://github.com/PolarBean/DeepSlice), ... | 
| [cellprofiler](https://cellprofiler.org/) | Open-source software designed to enable biologists to quantitatively measure phenotypes from thousands of images automatically. | 
| [cellpose](https://cellpose.readthedocs.io/en/latest/index.html#) |  An anatomical segmentation algorithm, to detect nucleus, cells, and much more ! | 
| [devbio-napari](https://github.com/haesleinhuepf/devbio-napari) | The Fijiest way to do image analysis in Python | 
| [EMPanADA](https://empanada.readthedocs.io/en/latest/)| DNN to segment mitochondria in EM images |
| [Fiji](https://fiji.sc/) | A “batteries-included” ImageJ  | update sites : clij, stardist, ptbiop , ilastik … |
| [ilastik (GPU)](https://www.ilastik.org/) | Interactive learning and segmentation toolkit | GPU version|
| [inkscape](https://inkscape.org/) |  Vectoriel drawing (and more!) | with [inkscape-imagej-panel](https://gitlab.com/doctormo/inkscape-imagej-panel) plugins |
| [QuPath](https://qupath.github.io/) | Digital Pathology | with some extensions : [cellpose](https://github.com/BIOP/qupath-extension-cellpose), [SAM](https://github.com/ksugar/qupath-extension-sam) , [Warpy](https://imagej.net/plugins/bdv/warpy/warpy) , [StarDist]()... |
| [StarDist](https://github.com/stardist/stardist) | Object Detection with Star-convex Shapes |
