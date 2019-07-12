---
layout: project
title: MaskFusion_cpp: Dense 3D Mapping Based on ElasticFusion and Mask-RCNN
date: Dec 14, 2018
image: /portfolio/public/images/MaskFusion cpp/pipeline.png
---

## Demo Video

<iframe width="560" height="315" src="https://www.youtube.com/watch?v=9d0Szh7lkns" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
-------------------------------------------------------------
     
## Project Goal
The goal of this project is to build a simultaneously localization and semantic mapping (SLAM) system.

### Pipeline:
- A real-time dense visual SLAM ([ElasticFusion](https://github.com/mp3guy/ElasticFusion)) system to generate surfel map.

- A segmentor based on [Mask-RCNN](https://www.youtube.com/watch?v=OOT3UIXZztE) to do semantic segmentation on input 2D RGB streams, and then project semantic segmentation label from 2D pixel to surfel on 3D dense map.

- A bayesian update scheme to refresh the semantic segmentation results on existing surfels.

The source code is [here](https://github.com/msr-peng/maskfusion_cpp).

The details about MaskFusion_cpp will be uploaded today.

