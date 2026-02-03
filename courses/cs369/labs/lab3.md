# CS369 Lab 3: Iterative IK and Control

## Overview
The goals of this lab:
- Practice computing the Jacobian matrix from the robot's forward kinematics.
- Implement an iterative inverse kinematics solver based on the Jacobian matrix.
- Implement and tune PID controllers to control a robot arm in simulation.

*Credit: Based on materials created by Zenas Boamah and Lei Lei.*

## Introduction
Inverse kinematics (IK) is the problem of finding robot joint configuration(s) to achieve a desired end effector position. In many cases, closed-form solutions are either unavailable or tedious to compute. We can instead perform **iterative IK** to compute the solution: starting with the current configuration, iteratively update the joint angles until the end effector reaches the target position within a tolerance.

In this lab, you will derive the equation for and implement a function to compute the Jacobian matrix given the robot configuration. You will also implement a Jacobian-based iterative IK solver and PID controllers to control a robot arm in simulation. You will work with the same three-link robot in 3D space as described in Lab 2.

## Part 1: Iterative IK
Given a target end effector position, we can compute a target end effector velocity:

$$\frac{dp}{dt} = \frac{dF(q)}{dt} = \frac{dF(q)}{dq}\frac{dq}{dt}$$

where $p$ is the end effector position, $F$ is the robot's forward kinematics function, and $q$ represents the joint configuration.

The Jacobian matrix is the derivative of the forward kinematics function with respect to the joint configuration: $J(q)=\frac{dF(q)}{dq}$. If we can compute $J(q)$, then we can calculate the target joint angle velocities from the target end effector velocity:

$$\frac{dp}{dt} = J(q)\frac{dq}{dt} \Leftrightarrow \frac{dq}{dt}=J^{-1}(q)\frac{dp}{dt}$$

We can iteratively update the joint angles based on $dq$. Note that the values for $J(q)$ and $dp$ will need to be updated along with the new joint angles.

Extend your `Robot` class from Lab 2 to include a `compute_Jacobian()` function that calculates the Jacobian matrix from the joint configuration. Also implement an `inverse_kinematics_3d(x,y,z,alpha,epsilon)` function that uses iterative IK to calculate and return as a list a joint configuration (in degrees) for the end effector to be at the given $(x,y,z)$ position within the $\epsilon$ tolerance. Return `None` if a solution does not exist.

In case the Jacobian matrix is not invertible, you can use the [`numpy.linalg.pinv()`](https://numpy.org/doc/2.1/reference/generated/numpy.linalg.pinv.html) function to calculate its pseudo-inverse. You will also need to experiment with the values of the step size $\alpha$ and tolerance $\epsilon$ to ensure efficient convergence (distance between the end effector and its target position is at most $0.001$).

## Part 2: Robot Control
A controller tells the robot how to move by calculating and sending control signals to the robot's motors. In the provided `pid.py` file, implement a PID controller based on the difference between the robot's current and goal joint configuration. The goal configuration should be computed by your `inverse_kinematics_3d()` function from a given target end effector position.

We will use [MuJoCo](https://mujoco.org/) to simulate the movement of our three-link robot.
Run the command below on a lab machine to set up a virtual environment `robvenv` with MuJoCo installed. Run `source ~/robvenv/bin/activate` to access the virtual environment, and `deactivate` to leave it.
```
bash /homes/students/robvenv_self-service.sh
```

You have been given starter code in `control.py` to interact with the simulator, which tracks the robot's joint angles (given in radians) and lets you send control signals to the robot's motors.

You will need to tune the gains of your PID controllers to move the robot to the desired joint configuration with high accuracy and stability (the robot should reach the goal configuration with minimal oscillation within 80 seconds or less). The recommended order of tuning is $K_p$ followed by $K_i$ then $K_d$. In the README file, record your observations of the effects of each gain parameter on the robot's movements.

## Deliverables
- Your derivation for the Jacobian matrix from the robot's forward kinematics (either typed up or a photo of your handwritten work is sufficient).
- Test cases for your `compute_Jacobian()` and `inverse_kinematics_3d()` functions.
- Plots showing your PID controllers' performances (created using the provided visualization function).
- Answers for the README questions.