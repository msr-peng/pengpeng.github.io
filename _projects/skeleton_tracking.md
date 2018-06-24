---
layout: project
title: Modern Skeleton Tracking Benchmarking
date: Jun 19, 2018
image: /portfolio/public/images/Skeleton Tracking/SkeletonTracing.jpg
---

## Project Goal
This project is going to explore a avriety new technologies about skeleton tracking, and to benchmard their performance in terms of accuracy, computational effort, and hardware requirements. And then develop user manuals and tutorials to accompany the results.

## Selected Solutions of skeleton tracking
**XBOX 360 Kinect + OpenNi_tracker + NITE + Linux**
     
Recommand Operating System and Architectures;
- Ubuntu 14.04 or 16.04

Recommended Hardware Configuration:
- 32-bit (x86) or 64-bit (x64) processor
- Dual-core 2.66-GHz or faster processor
- Dedicated USB 2.0 bus
- 2 GB RAM
- A Microsoft Kinect for Windows sensor

Software Requirement:
- OpenNI-Bin-Dev-Linux-x64-v1.5.7.10
- NITE-Bin-Linux-x64-v1.5.2.23
- SensorKinect093-Bin-Linux-x64-v5.1.2.1

Kinect V1 can simultaneously track 2 persons within 20 key joints points.
This solution can given the skeleton tracking result as `tf` data format in ROS, and visualize corresponding joint coordinate in `rviz`.
![Real-time Person](/portfolio/public/images/Skeleton Tracking/skeleton_1.gif)

Comparison between official development package and unofficial development package for **Kinect v1**:
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

Pros:
- Little computational requirements.
- High frequency of refreshment of the tracking result and little latency.

Cons:
- It can only track at most two person.
- It only works fine when peopel in a appropriate distance from Kinect(larger than two meters).
- The tracking result not robust when person's limbs overlap highly.

**Xtion PRO LIVE + OpenNI + NITEv2 + Linux**

**XBOX ONE Kinect + Microsoft SDK + OpenCV + Windows**
     
Supported Operating Systems and Architectures:
- Windows 8 (x64)
- Windows 10 (x64)

Recommended Hardware Configuration:
- 64 bit (x64) processor
- 4GB Memory (or more)
- I7 3.1 GHz (or higher)
- Built-in USB 3.0 host controller (Intel or Renesas chipset)
- DX11 capable graphics adapter
- A Kinect v2 sensor, which includes a power hub and USB cabling

Software Requirements:
- Visual Studio 2017
- OpenCV 3.4.1

Kinect v2 can simultaneously track 6 persons within 25 key joints points, which is much better than Kinect v1. Moreover, it has more roboust skeleton tracking result of signle person than Kinect v1.
This solution is developed by the combination of [Kinect for Windows SDK v2 C++ API](https://docs.microsoft.com/en-us/previous-versions/windows/kinect/hh855364(v%3dieb.10)) and [OpenCV 3.4.1](https://opencv.org/opencv-3-4-1.html) library, in [Visual Studio 2017](https://visualstudio.microsoft.com/zh-hans/vs/?rr=https%3A%2F%2Fwww.google.com%2F) IDE.
I extracted the color frame streams and the real-time data of skeleton tracking from Windows SDK v2 C++ API, and then drew the skeleton lines on color image streams within OpenCV. Here is the demo(The C++ source code is [here](https://github.com/KHeresy/KinectForWindows2Sample/blob/v2-naming/08cv_Body/cvBody.cpp). PS: window at the top left corner is the original depth & skeleton tracking result show in Kinect Studio v2.0):
![Kinect v2 result]()
My next step is to implement the interaction between Windows and Linux, and finally realize the 3-D skeleton reconstruction on Rviz. A potential solution to realize the interatcion between Windows and ROS on Linux is by [rosserial_windows](http://wiki.ros.org/rosserial_windows) package.

**OpenPose + RGBD Camera/FLIR Camera + Windows/Linux**
[OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose) is the first real-time multi-person system to jointly detect human body, hand, and facial keypoints(in total 130 keypoints) on single images.
It can give robust skeleton tracking result given RGB video about real-world persons or even animation person:
![Real-time Person](/portfolio/public/images/Skeleton Tracking/skeleton_4_1.gif)

![Animation Person](/portfolio/public/images/Skeleton Tracking/skeleton_4_2.gif)
Pros:
- It can tracking multiple persons.
- Skeleton tracking result is pretty robust to varying environmental conditions.(limbs overlap, lighting, clothing).
- It can tracking virtual person in games and animations.

Cons:
- High computational requirments.(It can only process approximate single image per 3 seconds in the condition of **Intel CORE i7 CPU**).

My following goal for this solution is to gets the coordinate data of user key points, thus realize 3-D reconstruction of human body, and finally user-mimicking deomstration(Baxter). By far I found there are three potential solutions(list by hardware requirements):
- Assume the person's body faced the camera directly(the plane where the person's body on is perfect vertical to the line formmed by the camera and person), so a demension of body joints' coordinates is fixed. Then we get the coordinates of body joints directly from image pixel, and feed it into **Baxter**. [Here](https://www.youtube.com/watch?v=wNLuZNLBegw) is similar work on **Robotis**.(RGB camera is enough)
- Use RGBD to get the registration point cloud of user, and then use the camera intrinsics and extrinsics to map the 2D pixel coordinates to corresponding 3D points in the camera space. [Here](https://github.com/IntelRealSense/librealsense/blob/master/include/librealsense2/rsutil.h)  is associated 2D to 3D projection functions of **Intel RealSense**.(RGBD camera is required)
- Implement built-in [OpenPose 3-D Reconstruction](https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/3d_reconstruction_demo.md) directly, and get the data of joints coordinate and feed it into **Baxter**.(FLIR Camera is required, and can only track one person)

The requirement of hardware is increasingly higher in order, but the results of joints coordinate is also increasingly higher.
