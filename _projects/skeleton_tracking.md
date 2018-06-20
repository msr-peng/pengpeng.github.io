---
layout: project
title: Modern Skeleton Tracking Benchmarking
date: Jun 19, 2018
image: /portfolio/public/images/turtlebot-3.jpg
---

![Follow Lane Line](/portfolio/public/images/Final Result/follow_lane.gif)

## Project Goal
This project is going to explore a avriety new technologies about skeleton tracking, and to benchmard their performance in terms of accuracy, computational effort, and hardware requirements. And then develop user manuals and tutorials to accompany the results.

## Selected Solutions of skeleton tracking
**XBOX 360 Kinect + OpenNi_tracker + NITE + Linux**
This solution can given the skeleton tracking result as `tf` data format in ROS, and visualize corresponding joint coordinate in `rviz`.
![Real-time Person](/portfolio/public/images/Skeleton Tracking/skeleton_1.gif)
Pros:
- Little computational requirements.
- High frequency of refreshment of the tracking result and little latency.

Cons:
- It can only track at most two person.
- It only works fine when peopel in a appropriate distance from Kinect(larger than two meters).
- The tracking result not robust when person's limbs overlap highly.

**XBOX ONE Kinect + Microsoft SDK + Windows**
Can not found the XBOX ONE Kinect adapter in MSR LAB. I will finish this parts once can make XBOX ONE Kinect work.

Comparison between official development package and unofficial development package for **Kinect**:
Official SDK:
Pros:
- Audio support.
- Multiple sensor(Kinect) support.
- Have higher accuracy in non-standard pose estimation.

Cons:
- Limitation on the business usage.
- Doesn't have gesture recognition and tracking functionality.
- Doesn't match the RGB image and depth image.

OpenNI/NITE:
Pros:
- Business usage support.
- Matching RGB image and depth image.
- Including gesture recognition and tracking functionality.

Cons:
- Doesn't support audio.
- Require standard pose to start skeleton tracking.
- Can't support multiple sensor(Kinect) work simultaneously.

**Xtion PRO LIVE + OpenNI + NITEv2 + Linux**

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
- Assume the person's body faced the camera directly(the plane where the person's body on is perfect vertical to the line formmed by the camera and person), so a demension of body joints' coordinates is fixed. Then we get the coordinates of body joints directly from image pixel, and feed it into **Baxter**. ![Here](https://www.youtube.com/watch?v=wNLuZNLBegw) is similar work on **Robotis**.(RGB camera is enough)
- Use RGBD to get the registration point cloud of user, and then use the camera intrinsics and extrinsics to map the 2D pixel coordinates to corresponding 3D points in the camera space. ![Here](https://github.com/IntelRealSense/librealsense/blob/master/include/librealsense2/rsutil.h)  is associated 2D to 3D projection functions of **Intel RealSense**.(RGBD camera is required)
- Implement built-in ![OpenPose 3-D Reconstruction](https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/3d_reconstruction_demo.md) directly, and get the data of joints coordinate and feed it into **Baxter**.(FLIR Camera is required, and can only track one person)

The requirement of hardware is increasingly higher in order, but the results of joints coordinate is also increasingly higher.
