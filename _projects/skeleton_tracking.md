---
layout: project
title: Modern Skeleton Tracking Benchmarking
date: Jun 19, 2018
image: /portfolio/public/images/Skeleton Tracking/SkeletonTracing.jpg
---
    
## Project Goal
    
This project is going to explore a avriety new technologies about skeleton tracking, and to benchmard their performance in terms of accuracy, computational effort, and hardware requirements. And then develop user manuals and tutorials to accompany the results.

-------------------------------------------------------------

## Related Hardware & Development Environment Introduction
    
In general, the selectivity of your skeleton tracking development enviroment mainly depends on which depth sensor you choose. So I list the possible development environment based on different depth sensors in form of table as follow:
    
![possible development environment choice](/portfolio/public/images/Skeleton Tracking/hardware_software.png)
    
---------------------------------------------------------------

**Microsoft Kinect (first generation)**
    
The appearance of product is as follow, which is the earliest depth sensor product:
    
![Kinect v1 camera](/portfolio/public/images/Skeleton Tracking/kinect_v1.jpg)
    
To get the depth information, it employes [PrimeSense](https://en.wikipedia.org/wiki/PrimeSense)'s Light Coding technology. It actually has two product: [Kinect for XBOX 360](https://support.xbox.com/en-US/xbox-360/accessories/kinect-sensor-components) and [Kinect for Windows](https://support.xbox.com/en-US/xbox-on-windows/accessories/kinect-for-windows-info). The former can be used on XBOX 360 as well as PC, while the latter can only used on PC.
If you choose Kinect (first generation), you have following development environment to choose:
    
- **OpenNI 1**:
    - An very old development environment
    - Cross-platform
    - Need driver from 3rd party, which is exclusive with [Kinect for Windows SDK v1](https://www.microsoft.com/en-us/download/details.aspx?id=28782)
- **OpenNI 2**:
    - Need to work with [Kinect for Windows SDK v1](https://www.microsoft.com/en-us/download/details.aspx?id=28782), which means it can only work on system later than Windows 7
    - Can work with [OpenNI2-FreenectDriver](https://github.com/OpenKinect/libfreenect/tree/master/OpenNI2-FreenectDriver) on non-Windows platform
- **Kinect for Windows SDK 1**:
    - Only can work on platform later than Windows 7
    
**Note**: Kinect (first generation) can not work with [Kinect for Windows SDK 2](https://www.microsoft.com/en-us/download/details.aspx?id=44561)!

---------------------------------------------------------------

**Microsoft Kinect (second generation)**
    
The appearance of the product is as follow:
    
![Kinect v2 camera](/portfolio/public/images/Skeleton Tracking/kinect_v2.png)
    
It start to use Microsoft own Time of Flight technology to get depth information. It also has two version, one is specific for Windows, the other is specific for XBOX One, but they are generally the same in functionality. It has following development environment to choose:
    
- **Kinect for Windows SDK v2**:
    - The most popular development environment for Kinect camera (second generation)
    - Can only work with USB 3.0 port
    - Can only work on platform latter than Windows 8

- **OpenNI 2**:
    - Can not work with NiTE, which means it can only get RGB & depth info, instead of skeleton keypoints info
    - Can work with OpenNI2 and [libfreenect2](https://github.com/OpenKinect/libfreenect2) on non-Windows platform, but it still can not get skeleton info

---------------------------------------------------------------

**AUSU Xtion series or other PrimeSense depth sensor**
    
Those depth sensor in general work with OpenNI 1 or OpenNI2
    
![Xtion Pro Live camera](/portfolio/public/images/Skeleton Tracking/xtion_pro_live.jpg)

---------------------------------------------------------------

## Selected Solutions of Skeleton Tracking
    
### Solutions Github Repository
1. [openni2_tracker](https://github.com/msr-peng/openni2_tracker)
    
2. [kinect_v2_skeleton_tracking](https://github.com/msr-peng/kinect_v2_skeleton_tracking)
    
3. [openpose_ros](https://github.com/msr-peng/openpose_ros)
    
**Note**: I didn't create github repository for the first solution (which I believe is easy enough to follow 3rd party instruction).
    
---------------------------------------------------------------
    
#### 1. XBOX 360 Kinect + OpenNi_tracker + NITE + Linux
     
**System Requirements**(taken from [Microsoft SDK v1.8](https://www.microsoft.com/en-us/download/details.aspx?id=40278) website.)
     
1. Recommand Operating System and Architectures;
- Ubuntu 14.04 or 16.04

2. Recommended Hardware Configuration:
- 32-bit (x86) or 64-bit (x64) processor
- Dual-core 2.66-GHz or faster processor
- Dedicated USB 2.0 bus
- 2 GB RAM
- A Microsoft Kinect for Windows sensor

3. Software Requirement:
- OpenNI-Bin-Dev-Linux-x64-v1.5.7.10
- NITE-Bin-Linux-x64-v1.5.2.23
- SensorKinect093-Bin-Linux-x64-v5.1.2.1

**Build development environment**
    
Solution 1's development environment is the easist one to build. To learn how to build the development environment, please follow the guide [here](https://www.reddit.com/r/ROS/comments/6qejy0/openni_kinect_installation_on_kinetic_indigo/).
    
**Introduction**
    
Kinect V1 can simultaneously track 2 persons(within XBox 360) within 20 key joints points.
This solution can given the skeleton tracking result as `tf` data format in ROS, and visualize corresponding joint coordinate in `rviz`.
    
![Real-time Person](/portfolio/public/images/Skeleton Tracking/skeleton_1.gif)

Comparison between official development package and unofficial development package for Kinect v1:
     
Official SDK:
Pros:
- Audio support.
- Multiple sensor(Kinect) support.
- Have higher accuracy in non-standard pose estimation.

OpenNI/NITE:
Pros:
- Business usage support.
- Matching RGB image and depth image.
- Including gesture recognition and tracking functionality.

Evaluation of Solution 1:
     
Pros:
- Little computational requirements.
- High frequency of refreshment of the tracking result and little latency.

Cons:
- It can only track at most two person.
- It only works fine when peopel in a appropriate distance from Kinect(larger than one meter).
- The tracking result not robust when person's limbs overlap highly.
- At the start of skeleton tracking, use need to do "surrendering" pose.
   
---------------------------------------------------------------
    
#### 2. Xtion PRO LIVE + OpenNI2 + NITEv2.2 + Linux

**System Requirements**
    
1. Recommand Operating System and Architectures;
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
    
To learn how to build solution 2's development environment or access corresponding docker image file directly, please follow my corresponding github repository [openni2_tracker](https://github.com/msr-peng/openni2_tracker).

Evaluation of Solution 2 based on Solution 1:
    
Pros:
- User needn't to do "surrender" pose at the begining of skeleton tracking
- Xtion Pro Live is much more light than Kinect camera (first generation)

Cons:
- The skeleton tracking result is a little unstable
    
---------------------------------------------------------------
    
#### 3. XBOX ONE Kinect + Microsoft SDK + OpenCV + Windows
     
**System Requirements**(taken from [Microsoft SDK 2.0](https://www.microsoft.com/en-us/download/details.aspx?id=44561) website.)
     
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
    
Kinect v2 can simultaneously track 6 persons within 25 key joints points, which is much better than Kinect v1. Moreover, it has more roboust skeleton tracking result of signle person than Kinect v1.
This solution is developed by the combination of [Kinect for Windows SDK v2 C++ API](https://docs.microsoft.com/en-us/previous-versions/windows/kinect/hh855364(v%3dieb.10)) and [OpenCV 3.4.1](https://opencv.org/opencv-3-4-1.html) library, in [Visual Studio 2017](https://visualstudio.microsoft.com/zh-hans/vs/?rr=https%3A%2F%2Fwww.google.com%2F) IDE.
    
Evaluation of Solution 3 based on Solution 2:
    
Pros:
- Skeleton tracking result is a little more robust
- Windows SDK v2 has a lot of C++ API, which support we acquire data more than skeleton tracking

**My Work**:
    
I extracted the color frame streams and the real-time data of skeleton tracking from Windows SDK v2 C++ API, and then drew the skeleton lines on color image streams within OpenCV. Here is the demo(The C++ source code is [here](https://github.com/KHeresy/KinectForWindows2Sample/blob/v2-naming/08cv_Body/cvBody.cpp). PS: window at the top left corner is the original depth & skeleton tracking result show in Kinect Studio v2.0):
![Kinect v2 result](/portfolio/public/images/Skeleton Tracking/skeleton_3.gif)
    
I implemented the interaction between Windows and Linux within little lag by [rosserial_windows](http://wiki.ros.org/rosserial_windows) package. Then I get the 3D skeleton tracking date from Windows Kinect v2, and visualized them on Ubuntu Rviz.
    
---------------------------------------------------------------
    
#### 4. OpenPose + RGBD Camera/FLIR Camera + Windows/Linux
    
**System Requirements**(taken from [OpenPose Github Page](https://github.com/CMU-Perceptual-Computing-Lab/openpose))
1. Nvidia GPU version:
- NVIDIA graphics card with at least 1.6 GB available (the `nvidia-smi` command checks the available GPU memory in Ubuntu)l
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
It can give robust skeleton tracking result given RGB video about real-world persons or even animation person:
    
![Real-time Person](/portfolio/public/images/Skeleton Tracking/skeleton_4_1.gif)
    
Evaluation of Solution 4 based on Solution 3:
Pros:
- Even if there is some obstruct in front of the person, OpenPose can still give a good prediction of the skeleton keypoints behind the obstruct. 
- It can tracking virtual person in games and animations.
    
Cons:
- High computational requirments.(It can only process approximate single image per 3 seconds in the condition of **Intel CORE i7 CPU**); On GTX 1060, I can arrive 10 fps; On 4*GTX 1080 Ti, I can arrive 15 fps.
- The skeleton tracking result is not so robust when light condition is bad.
    
**My Work**:
    
I employed OpenPose C++ APIs to make it do inference on 2D RGB streams, then got the pixel coordinate of skeleton keypoints. Then I applied camera instrinc parameter to do some simple geometry transformation, finally get the 3D skeleton keypoints information, and visualized on Rviz.
    
Here is the demo of 3D skeleton tracking by OpenPose (approximately 15 fps within 4* GTX 1080 Ti):
    
![OpenPose 3D](/portfolio/public/images/Skeleton Tracking/openpose_3d.gif)
    
---------------------------------------------------------------
    
## Experiments & Comparison
    
I also compare the robust of skeleton tracking results between depth method (Solution 1 & 2 & 3) and RGB method (Solution 4) in following 3 extreme condition:
- Obstruct in front of the person
- Dark environment
- Overlap of multiple persons
    
I found that skeleton tracking solutions based on depth information is more robust to dark environment, while skeleton tracking solution based on RGB information does better in the first and third extreme condition.
    
Here is the comparsion of skeleton tracking results:
    
**Obstruct in front of the person**:
    
Depth Solution (1 & 2 & 3)                                       |  RGB Solution (4)
:---------------------------------------------------------------:|:----------------------------------------------------------------:
![](/portfolio/public/images/Skeleton Tracking/obstruct.gif)     |  ![](/portfolio/public/images/Skeleton Tracking/obstruct_op.gif) 
    
Apparently OpenPose performance is much better than depth solution when there is obstruct in front of person. That's because depth solutions use object nearest it to judge whether it's person or not, so obstruct in front of people can fool depth solution very easily. While OpenPose use RGB information to judge, it can infer the body parts behind the obstruct with support of neural network.
    
**Dark environment**:
    
Depth Solution (1 & 2 & 3)                                       |  RGB Solution (4)
:---------------------------------------------------------------:|:----------------------------------------------------------------:
![](/portfolio/public/images/Skeleton Tracking/dark.gif)         |  ![](/portfolio/public/images/Skeleton Tracking/dark_op.gif)
    
In dark environment, depth solutions' performance are much better than RGB solution (OpenPose). That because when light is not enough, it will cause huge disturb on RGB information, while it has no influence on depth information at all.
    
**Overlapping persons**:
    
I didn' find MSR cohort to do experiments with me, but I believe OpenPose should do better in such condition, the reason is the same as obstruct.
    
---------------------------------------------------------------

## Stretch Goal
    
My stretch goal is to do skeleton tracking in large scene by fusion the data provided by asynchronous OpenPose clients. [Here](https://arxiv.org/pdf/1710.06235.pdf) is realed paper.
