---
layout: project
title: Modern Skeleton Tracking Benchmarking
date: Jun 19, 2018
image: /portfolio/public/images/Skeleton Tracking/SkeletonTracing.jpg
---

## Demo Video

<iframe width="560" height="315" src="https://www.youtube.com/embed/f2FjMg06Vbg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
-------------------------------------------------------------
    
## Project Goal
    
This project explore a variety of new skeleton tracking technologies. It benchmarks
 accuracy, computing resources, and hardware requirements. The project develops user manuals and tutorials to accompany the results.

-------------------------------------------------------------

## Hardware & Development Environment
    
In general, the selectivity of skeleton tracking development enviroment depends on the depth sensor you choose. The following is a table of development environments based on different depth sensors.
    
![possible development environment choice](/portfolio/public/images/Skeleton Tracking/hardware_software.png)
    
Kinect V1                                                         |  Kinect V2                                                       |  AUSU Xtion Pro Live
:----------------------------------------------------------------:|:----------------------------------------------------------------:|:----------------------------------------------------------------:
![](/portfolio/public/images/Skeleton Tracking/kinect_v1.jpg)     |  ![](/portfolio/public/images/Skeleton Tracking/kinect_v2.jpg)   |  ![](/portfolio/public/images/Skeleton Tracking/xtion_pro_live.jpg) 
    
---------------------------------------------------------------

**Microsoft Kinect (first generation)**
    
To get the depth information, it employes [PrimeSense](https://en.wikipedia.org/wiki/PrimeSense)'s Light Coding technology. There is two version of products: [Kinect for XBOX 360](https://support.xbox.com/en-US/xbox-360/accessories/kinect-sensor-components) and [Kinect for Windows](https://support.xbox.com/en-US/xbox-on-windows/accessories/kinect-for-windows-info). The former can be used on XBOX 360 and a PC, while the latter is PC only.
The following are development environments for Kinect first generation:
    
- **OpenNI 1**:
    - A very old development environment.
    - Cross-platform.
    - Requires 3rd party driver which is incompatible with [Kinect for Windows SDK v1](https://www.microsoft.com/en-us/download/details.aspx?id=28782).
- **OpenNI 2**:
    - Requires [Kinect for Windows SDK v1](https://www.microsoft.com/en-us/download/details.aspx?id=28782), and Windows 7 or greater.
    - Works with [OpenNI2-FreenectDriver](https://github.com/OpenKinect/libfreenect/tree/master/OpenNI2-FreenectDriver) on non-Windows platforms.
- **Kinect for Windows SDK 1**:
    - Requires Windows 7 or greater.
    
**Note**: Kinect (first generation) incompatible with [Kinect for Windows SDK 2](https://www.microsoft.com/en-us/download/details.aspx?id=44561)!

---------------------------------------------------------------

**Microsoft Kinect (second generation)** 
    
The second generation uses Microsoft own Time of Flight technology for depth generation. There has two version, one is specific for Windows, the other is specific for XBOX One, they generally share the same functionality.
    
Development environemnts:
    
- **Kinect for Windows SDK v2**:
    - The most popular development environment for Kinect camera (second generation)
    - Requires USB 3.0 port
    - Requires Windows 8 or greater

- **OpenNI 2**:
    - doesn't work with NiTE, it lacks skeleton keypoints information.
    
    - works with OpenNI2 and [libfreenect2](https://github.com/OpenKinect/libfreenect2) on non-Windows platforms, but still lacks skeleton information.

---------------------------------------------------------------

**AUSU Xtion series or other PrimeSense depth sensor**
    
Requires OpenNI 1 or OpenNI2.

---------------------------------------------------------------

## Selected Solutions of Skeleton Tracking
    
### Github Repository
1. [openni2-tracker](https://github.com/msr-peng/openni2-tracker)
    
2. [kinect_v2_skeleton_tracking](https://github.com/msr-peng/kinect_v2_skeleton_tracking)
    
3. [openpose_ros](https://github.com/msr-peng/openpose_ros)
    
---------------------------------------------------------------
    
#### 1. XBOX 360 Kinect + OpenNi_tracker + NITE + Linux
     
**System Requirements**(taken from [Microsoft SDK v1.8](https://www.microsoft.com/en-us/download/details.aspx?id=40278) website.)
     
1. Recommanded Operating System:
- Ubuntu 14.04 or 16.04

2. Recommended Hardware Configuration:
- 32-bit (x86) or 64-bit (x64) processor
- Dual-core 2.66-GHz or faster processor
- Dedicated USB 2.0 bus
- 2 GB RAM
- A Microsoft Kinect for Windows sensor

3. Software Requirements:
- OpenNI-Bin-Dev-Linux-x64-v1.5.7.10
- NITE-Bin-Linux-x64-v1.5.2.23
- SensorKinect093-Bin-Linux-x64-v5.1.2.1

**Build development environment**
    
Solution 1's development environment is the easist one to build. To learn how to build the development environment, please follow the guide [here](https://www.reddit.com/r/ROS/comments/6qejy0/openni_kinect_installation_on_kinetic_indigo/).
    
**Introduction**
    
Kinect V1 can simultaneously track 2 persons(within XBox 360) within 20 key joints points.
This solution gives skeleton tracking result as `tf` data format in ROS, and visualizes corresponding joint coordinates in `Rviz`.
    
![Real-time Person](/portfolio/public/images/Skeleton Tracking/skeleton_1.gif)

Comparison between official development package and unofficial development package for Kinect v1:
     
Official SDK:
Pros:
- Audio support.
- Multiple sensor(Kinect) support.
- higher accuracy in non-standard pose estimation.

OpenNI/NITE:
Pros:
- Open-sourced.
- Matching RGB image and depth image.
- Gesture recognition and tracking.

Evaluation of Solution 1:
     
Pros:
- Little computational requirements.
- High refresh rate, low latency for tracking results.

Cons:
- Max two people.
- Requires distence greater than one meter from Kinect.
- Tracking no robust when person's limbs greatly overlap.
- Rquires "psi" pose to initialize skeleton tracking.
   
---------------------------------------------------------------
    
#### 2. Xtion PRO LIVE + OpenNI2 + NITEv2.2 + Linux

**System Requirements**
    
1. Recommand Operating System:
- Ubuntu 14.04 or 16.04

2. Recommended Hardware Configuration:
- 32-bit (x86) or 64-bit (x64) processor
- Dual-core 2.66-GHz or faster processor
- Dedicated USB 2.0 bus
- 2 GB RAM

3. Software Requirement:
- OpenNI-Bin-Dev-Linux-x64-v2
- NITE-Bin-Linux-x64-v2.2
- libopenni-sensor-primesense0

**Build development environment**
    
To learn how to build solution 2's development environment or access corresponding docker image file directly, please follow my corresponding github repository [openni2-tracker](https://github.com/msr-peng/openni2-tracker).

Evaluation of Solution 2 based on Solution 1:
    
Pros:
- No "psi" pose to initialize skeleton tracking.
- Xtion Pro Live is significantly lighter than Kinect camera (first generation).

Cons:
- The skeleton tracking is comparatively unstable.
    
---------------------------------------------------------------
    
#### 3. XBOX ONE Kinect + Microsoft SDK + OpenCV + Windows
    
**System Requirements**([Microsoft SDK 2.0](https://www.microsoft.com/en-us/download/details.aspx?id=44561) website.)
     
1. Supported Operating Systems and Architectures:
- Windows 8 (x64)
- Windows 10 (x64)

2. Recommended Hardware Configuration:
- 64 bit (x64) processor
- 4GB Memory (or more)
- I7 3.1 GHz (or higher)
- Built-in USB 3.0 host controller (Intel or Renesas chipset)
- DX11 capable graphics adapter
- A Kinect v2 sensor, which includes a power hub and USB cabling

3. Software Requirements:
- Visual Studio 2017
- OpenCV 3.4.1 (recommended)

**Build development environment**
    
To learn how to build solution 3's development environment, please follow my corresponding github repository [kinect_v2_skeleton_tracking](https://github.com/msr-peng/kinect_v2_skeleton_tracking).
     
**Introduction**
    
Kinect v2 can simultaneously tracks 6 people within 25 key joint points, which is much greater than Kinect v1. Moreover, it has more roboust skeleton tracking results for a signle person than Kinect v1.
The solution is developed by the combination of [Kinect for Windows SDK v2 C++ API](https://docs.microsoft.com/en-us/previous-versions/windows/kinect/hh855364(v%3dieb.10)) and [OpenCV 3.4.1](https://opencv.org/opencv-3-4-1.html) library, in [Visual Studio 2017](https://visualstudio.microsoft.com/zh-hans/vs/?rr=https%3A%2F%2Fwww.google.com%2F) IDE.
    
Evaluation of Solution 3 versus Solution 2:
    
Pros:
- Skeleton tracking result is a little more robust.
- Windows SDK v2 has C++ tracking APIs more than just skeleton tracking.

**My Work**:
    
I extracted color frames streams and real-time data of skeleton tracking using Windows SDK v2 C++ APIs, and drew the skeleton lines on color images streams within OpenCV. Here is the demo(The C++ source code is [here](https://github.com/KHeresy/KinectForWindows2Sample/blob/v2-naming/08cv_Body/cvBody.cpp). Note: window at the top left corner is the original depth & skeleton tracking result shown in Kinect Studio v2.0)
    
I implemented interaction between Windows and Linux minimize lag by using [rosserial_windows](http://wiki.ros.org/rosserial_windows) package. I then got 3D skeleton tracking date from Windows Kinect v2, and visualized them on Ubuntu Rviz.
    
---------------------------------------------------------------
    
#### 4. OpenPose + RGBD Camera/FLIR Camera + Windows/Linux
    
**System Requirements**([OpenPose Github Page](https://github.com/CMU-Perceptual-Computing-Lab/openpose))
1. Nvidia GPU version:
- NVIDIA graphics card with at least 1.6 GB available (the `nvidia-smi` command checks the available GPU memory in Ubuntu).
- At least 2.5 GB of free RAM memory for BODY_25 model or 2 GB for COCO model (assuming cuDNN installed).
- Highly recommended: cuDNN.
2. AMD GPU version:
- Vega series graphics card
- At least 2 GB of free RAM memory.
3. CPU version:
- Around 8GB of free RAM memory.
4. Highly recommended: a CPU with at least 8 cores.
    
**Build development environment**
    
To learn how to build solution 3's development environment or access corresponding docker image file directly, please follow my corresponding github repository [openpose_ros](https://github.com/msr-peng/openpose_ros).
    
**Introduction**
    
[OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose) is the first real-time multi-person system to jointly detect human body, hand, and facial keypoints(in total 130 keypoints) on single images.
    
Evaluation of Solution 4 versus 3:
Pros:
- When the person is occluded, OpenPose can give predictions of the skeleton keypoints behind the obstruction. 
- Tracks virtual persons in games and animations.
    
Cons:
- High computational requirements.(It only process approximately one image every 3 seconds on a **Intel CORE i7 CPU**); On a GTX 1060, it performs 10 fps; On 4*GTX 1080 Tis, 15 fps.
- The skeleton tracking result is not so robust when light conditions are bad.
    
**My Work**:
    
I employed OpenPose C++ APIs to do inference on 2D RGB streams, then got pixel coordinates of skeleton keypoints. I then applied camera instrinc parameters to do geometry transformation, got 3D skeleton keypoints information, and visualized on Rviz.
    
---------------------------------------------------------------
    
## Experiments & Comparison
    
Here I compare the robustness of skeleton tracking between depth methods (Solution 1 & 2 & 3) and RGB methods (Solution 4) in the following 3 extreme conditions:
- Obstruct in front of the person
- Dark environment
- Overlap of multiple persons
    
I found that skeleton tracking solutions based on depth information is more robust to dark environment, while skeleton tracking solution based on RGB information does better in the first and third extreme condition.
    
Here is the comparison of skeleton tracking results:
    
**Occluded person**:
    
Depth Solution (1 & 2 & 3)                                       |  RGB Solution (4)
:---------------------------------------------------------------:|:----------------------------------------------------------------:
![](/portfolio/public/images/Skeleton Tracking/obstruct.gif)     |  ![](/portfolio/public/images/Skeleton Tracking/obstruct_op.gif) 
    
OpenPose performs better than depth solutions when the person is occluded. That's because depth solutions use the object nearest to judge whether it's a person or not, so obstruction in front of people can fool depth solutions easily. While OpenPose uses RGB information to judge, it can infer the body parts behind the obstruction with support of neural networks.
    
**Dark environment**:
    
Depth Solution (1 & 2 & 3)                                       |  RGB Solution (4)
:---------------------------------------------------------------:|:----------------------------------------------------------------:
![](/portfolio/public/images/Skeleton Tracking/dark.gif)         |  ![](/portfolio/public/images/Skeleton Tracking/dark_op.gif)
    
In low light environments, depth solutions' perform better than RGB solution (OpenPose). That's because in low light, all depth information is preserved, but RGB information is not.
    
**Overlapping persons**:
    
I'm unable to test, but I believe OpenPose should perform better in such condition, due to its robustness when the subject is occluded.
    
---------------------------------------------------------------

## Stretch Goal
    
My stretch goal is to do skeleton tracking in large scenes by data fusion provided by asynchronous OpenPose clients. [Here](https://arxiv.org/pdf/1710.06235.pdf) is the related paper.
