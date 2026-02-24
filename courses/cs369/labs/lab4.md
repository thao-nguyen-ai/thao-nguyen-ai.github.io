# CS369 Lab 4: Motion Planning

## Overview
The goals of this lab:
- Implement motion planning algorithms.
- Practice working with the robot's configuration space.
- Assess tradeoffs between the different approaches to motion planning.
- Program a physical robot to carry out the motion planned paths.

*Credit: Based on materials created by Owen Bluman and Zenas Boamah.*

## Introduction
Motion planning is the problem of finding a path (i.e., sequence of configurations) for a robot to move from a start configuration to a goal configuration while avoiding obstacles in the environment. The two main approaches to motion planning is graph search and sampling-based algorithms. Graph search algorithms (e.g., Wavefront, A*) find paths by searching through a discretized representation of the environment. Conversely, sampling-based methods (e.g., RRT*) build paths from random samples of the robot's continuous configuration space.

###  Configuration Space (C-space)
**Definition**: The set of all possible configurations of the robot in the environment.

Within an environment, not all robot configurations are guaranteed to be valid or reachable. This could be due to obstacles occupying space in the environment, or the robot's shape and size, etc. For example, even when a room corner is free of obstacles, a Roomba robot will not be able to reach the furthest corner point because of its circular shape. It is important to consider the robot's configuration space when performing motion planning to ensure the output paths are collision-free.
 
For this lab, you will perform motion planning for circular robots in 2D rectangle maps. The robot's configuration is represented by the (x,y) coordinates of its center. To create the configuration space, we inflate the map's boundaries and obstacles by the robot's radius, then treat the robot as a point. You will also implement a movement script for the LeKiwi robot to follow the motion planned paths.

##  Part 1: Motion Planning Algorithms
Implement at least one graph search and one sampling-based motion planning algorithm of your choice. Your functions should take as input an instance of the provided `Problem` class and return a list of tuples representing the (x, y) coordinates along the planned path, including the robot's start and goal positions. Return an empty list if a solution does not exist.

We have implemented the creation of the robot's configuration space for you. An occupancy grid is the simplest discrete representation of the environment. Since the LeKiwi can move in any direction, you should use 8-connectivity for grid cell adjacency. For collision checking, we recommend using the [`shapely.intersects()`](https://shapely.readthedocs.io/en/stable/reference/shapely.intersects.html) function.

In the provided `motion_planning.py` file, we have included a `visualize()` function to display a visualization of the motion planning problem and other useful information. We recommend you use the visualizations and your own test cases to verify your algorithm implementations.

###  Evaluation
Your motion planning algorithms will be evaluated based on:
- Correctness of the output path (exists if and only if the goal is reachable from the starting position, and does not collide with any obstacles).
- Path optimality (measured by its Euclidean distance).
- Planning time.

To aid the evaluation, implement `compute_distance()` and `collision_check()` functions to calculate the Euclidean distance of the output path and check whether the path collides with any obstacles. Your code should also print out the amount of time your algorithms took to solve a motion planning problem.

We have provided a suite of motion planning problems in `motion_planning.py`. Analyze your motion planning algorithms' performance on the problems and record your observations in the README file. The algorithms should not take longer than 20 seconds to solve a problem, and the output path should not be longer than four times the straight-line distance between the start and goal positions. You can set the random seed to reproduce the results of your sampling-based algorithm.

## Part 2: Robot Movement Script

Modify `move.py` to control the LeKiwi's base, given a list of tuples representing the (x, y) coordinates along the planned path. The LeKiwi's initial position will be the starting point, and the coordinates will be in meters. The LeKiwi should move rightwards given a positive change in the x coordinate, and move forward given a positive change in the y coordinate. Note that you are implementing an open-loop controller as there is no feedback.

To test the script, place it in the `lerobot/examples/lekiwi` folder and run it similar to the [intructions](https://huggingface.co/docs/lerobot/lekiwi#teleoperate-lekiwi) for `teleoperate.py`.

## Deliverables
- Attend office or TA hours to demonstrate and get checked off for the movement script before the deadline.
- Well-commented functions.
- Test cases for your evaluation functions.
- Log of your algorithms' performance (planning time, path distance, and collision checking).
- Visualizations of the output paths (one per problem, with labels to distinguish the graph search and sampling-based paths).
- Answers for the README questions.
