---
layout: project
title: Self-driving Turtlebot3 Based on Advanced Lane Line Following and Traffic Sign Recognition
date: March 12, 2018
image: /portfolio/public/images/turtlebot-3.jpg
---

## Project Goal
This project is going to build a elementary self-driving robot, which can follow the lane lines and recognize the traffic signs it face to, and appropriately respond to signs such as "stop", "decelerate", "U turn", "keep left", "keep right", "go straight".

Here are the demos of final result("Keep Left", "Keep RIght", "Stop", "U-turn"):

<html>
<body>
        <table border="1">
            <tr>
                <td>
                    <img src="/portfolio/public/images/Final Result/left.gif" width="360px" height="360px" alt="" />
                </td>

                <td>
                    <img src="/portfolio/public/images/Final Result/right.gif" width="360px" height="360px" alt="" />
                </td>
            </tr>

            <tr>
                <td>
                    <img src="/portfolio/public/images/Final Result/stop.gif" width="360px" height="360px" alt="" />
                </td>

                <td>
                    <img src="/portfolio/public/images/Final Result/U_turn.gif" width="360px" height="360px" alt="" />
                </td>
            </tr>
        </table>
</body>
</html>
     
## Project Setup
The detector dataset is traffic sign sets (labeled 1) and non-traffic signs (labeled 2), with the following characteristics:
* Images are 32 (width) x 32 (height) x 3 (RGB color channels)
* Traffic sign set is composed of 26639 images, non-traffic sign (normal **MSR LAB** images) is composed of 25500 images
* Training set to test set is 0.8 : 0.2

The classifier dataset is plit into training, test and validation sets, with the following characteristics:
* Images are 32 (width) x 32 (height) x 3 (RGB color channels)
* Training set is composed of 39209 images 
* Validation set is composed of 2526 images
* Test set is composed of 10104 images
* There are 43 classes (e.g. Speed Limit 20km/h, No entry, Bumpy road, etc.)

Moreover, we will be using Python 2.7 with Tensorflow and OpenCV to write our code. And then drive the robot based on ROS platform.

## Project Architecture
**Advanced Lane Finding**
- Camera Calibration and Distortion Correction
- Thresholded binary image based on color transforms and gradients
- Perspective Transform (birds-eye view)
- Identifying the lane
- Computing lane’s curvature and center deviation
- PID controller based on curvature and center deviation

**Traffic Sign Detection**
- Detecting Feature Choice
- Building and Training Classifier
- Multi-scale Sliding Windows search
- Multiple Detections & False Positives

**Traffic Sign Classifier**
- Dataset Choice and Its Preprocess
- Deep CNN Architecture
- Dropout
- Data Augment

**Traffic Sign Behavior**
- Image Stream Preprocess
- Traffic Sign Behavior Realization

If you want to see the details of each steps and the python source code, please click [here](https://github.com/msr-peng/Self-Driving-Turtlebot3).
