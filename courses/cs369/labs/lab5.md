# CS369 Lab 5: Perception

## Overview
The goals of this lab:
- Understand and apply the pinhole camera model for object distance estimation.
- Practice working with an object detection model and computer vision techniques.
- Program a robot to follow a line with high accuracy and speed.

*Credit: Based on materials created by Owen Bluman and Howie Choset (CMU).*

## Part 1: Distance Estimation
Create a pipeline to take in images of known objects and determine the distance (in meters) to these objects. You can use the `LeKiwiClient.get_observation()` function to capture images using the LeKiwi's base camera, which has square pixels.

The pinhole camera model establishes a one-to-one mapping between points on the 3D object and the digital image, which can be used to calculate the distance to the object. To detect the object in the image, you can use [YOLO](https://docs.ultralytics.com/), a CNN-based object detection model. We recommend the pretrained [YOLO26n](https://docs.ultralytics.com/models/yolo26/#usage-examples) model. Run the command below on a lab machine to set up a virtual environment `robvenv` with YOLO installed:
```
bash /homes/students/robvenv_self-service.sh
```

Include in your code an explanation of the steps in your pipeline and the reasoning behind them (with at least one symbolic equation). Your pipeline will be evaluated on a variety of object types.

## Part 2: Line Detection and Following
One of the easiest ways to have a robot follow a certain path is to create a clear landmark that it can identify and follow. In the case of line-following, this is a colored line typically located under the robot that the robot can sense and use to determine where it should drive. Line-following was one of the first methods of mobile robot navigation.

You will be working on this part in pairs. Follow the instructions [here](https://docs.opencv.org/4.x/d6/d10/tutorial_py_houghlines.html) to detect lines in images and use that information to control the LeKiwi to follow a line. There are two main strategies for line-following:
- **Stay on the line:** Drive straight until you do not see the line. When you do not see the line, rotate in place until the line is detected.
- **Hug the side of the line:** If you see the line, curve in one direction. If you do not see the line, curve in the other direction.

## Deliverables
- Attend office or TA hours to demonstrate and get checked off for the line-following portion of the lab before the deadline.
- Well-commented functions.
- Test cases for your distance estimation pipeline.
- Answers for the README questions.

