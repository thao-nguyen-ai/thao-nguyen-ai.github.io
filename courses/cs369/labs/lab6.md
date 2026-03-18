# CS369 Lab 6: Localization

## Overview
The goals of this lab:
- Create a pipeline to enable the robot to take in environment information to inform itself about its position.
- Implement a probabilistic method to determine the robot's most likely position on a known map.

*Credit: Based on materials created by Howie Choset (CMU).*

## Part 1: Sensor Measurements
Extend your distance estimation pipeline from lab 5 to take in images of known objects and determine the object's range (in meters) and bearing (in radians) relative to the robot's local coordinate frame. Note that the camera's coordinate frame is usually different from the robot's frame.

<p align="center">
  <img src="figs/sensor.png" alt="sensor" width="250"/><br>
  <b>Figure 1:</b> Object's range and bearing relative to the camera's coordinate frame. <br>
</p>

Include in your code an explanation of the steps in your pipeline and the reasoning behind them (with at least three symbolic equations). Your pipeline should also output a signature for the object.

## Part 2: Localization
Localization is the process of determining the robot's pose relative to the environment map. For this lab, you will implement the Monte Carlo localization algorithm to determine the robot's location along a circular path. 

<p align="center">
  <img src="figs/demo.jpeg" alt="demo" width="400"/>
</p>

Your robot must follow the circular path. You may use your line-following code from lab 5. You should implement the velocity-based motion model and feature-based sensor model (with known correspondence) for localization. Note that the robot's heading angle should be constrained by its location on the circular path.


## Deliverables
- Attend office or TA hours to demonstrate and get checked off for the localization portion of the lab before the deadline.
- Well-commented functions.
- Test cases for your sensor measurements.
- Answers for the README questions.

