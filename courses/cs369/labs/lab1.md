# CS369 Lab 1: Robot Assembly and Setup

For this first lab, you will be assembling a LeKiwi robot with an SO101 arm. 
A kit will be provided to your group with all the materials and tools required for the assembly.
The TAs will closely monitor your progress, and will offer assistance especially in some of the more difficult parts of the assembly. We will also set up an FAQ post on Piazza to address common questions, challenges, or issues with assembly.

*Credit: Based on materials created by Matt Feinstein.*

## Part 1: Software Installation and Motor Configuration

- To install LeRobot on the Raspberry Pi, follow the instructions [here](https://huggingface.co/docs/lerobot/lekiwi#install-lerobot-on-pi-) and install from PyPI. Remember to install the `feetech` and `lekiwi` functionalities.

    To SSH into the Raspberry Pi, run the command below on a lab machine or your laptop (must be connected to the Haverford Eduroam network). Replace `X` with your given robot number:
    ```
    ssh robotX@robotX.haverford.edu
    ```

- Run the command below on a lab machine to set up a virtual environment `robvenv` with the necessary libraries. The path to the installed LeRobot package will be `/opt/lerobot-src`. Run `source ~/robvenv/bin/activate` to access the virtual environment, and `deactivate` to leave it.
    ```
    bash /homes/students/robvenv_self-service.sh
    ```

    To install LeRobot on your machine instead, follow the instructions [here](https://huggingface.co/docs/lerobot/lekiwi#install-lerobot-locally) and install from source. Remember to install the `feetech`, `lekiwi`, and `kinematics` functionalities.

- Follow the instructions [here](https://huggingface.co/docs/lerobot/lekiwi#configure-motors) to configure the motors with `--robot.port=/dev/ttyACM0`

    On the lab machines, the command to run the script is slightly different:
    ```
    python /opt/lerobot-src/src/lerobot/scripts/lerobot_setup_motors.py \
        --robot.type=lekiwi \
        --robot.port=/dev/ttyACM0
    ```

## Part 2: Assembly
Guides for the assembly are attached below: 

- [LeKiwi Base Assembly Guide](https://github.com/SIGRobotics-UIUC/LeKiwi/blob/main/Assembly.md)
- [SO101 Arm Assembly Guide](https://huggingface.co/docs/lerobot/en/so101#clean-parts)

Note that our robot is the 12v version, and we only have the follower arm. Follow the instructions [here](https://github.com/SIGRobotics-UIUC/LeKiwi/blob/main/Assembly.md#option-2-mounting-webcam) to mount the webcams to the robot.

> Please be careful with the 3D printed parts as they can break and are difficult to replace. We have some spare parts, but not many, so please handle them with caution.

## Part 3: Teleoperation
Calibrate the follower arm using [these instructions](https://huggingface.co/docs/lerobot/lekiwi#calibrate-follower-arm-on-mobile-base). Now you can teleoperate the robot using the instructions in the lab repository.

## Deliverables
- Attend office or TA hours to get checked off for the lab before the deadline. We will check the assembly and ask you to teleoperate the robot.
- I have reserved lockers in the Science Library for robot storage. After you have finished assembling the robot, contact [Carol Howe](https://calendly.com/carolhowe) for locker access.
- Answer README questions.