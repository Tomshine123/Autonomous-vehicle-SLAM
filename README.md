# My_project
This repository is my implementation for ME5413 Autonomous Mobile Robotics Final Project
>Main Authors: Zhang Ceng

![Ubuntu 20.04](https://img.shields.io/badge/OS-Ubuntu_20.04-informational?style=flat&logo=ubuntu&logoColor=white&color=2bbc8a)
![ROS Noetic](https://img.shields.io/badge/Tools-ROS_Noetic-informational?style=flat&logo=ROS&logoColor=white&color=2bbc8a)
![C++](https://img.shields.io/badge/Code-C++-informational?style=flat&logo=c%2B%2B&logoColor=white&color=2bbc8a)
![Python](https://img.shields.io/badge/Code-Python-informational?style=flat&logo=Python&logoColor=white&color=2bbc8a)
![GitHub Repo stars](https://img.shields.io/github/stars/Tomshine123/My_project?color=FFE333)

## Dependencies
The requirement can be found in https://github.com/Tomshine123/ME5413_Final_Project/blob/main/README.md
  * `pcl_ros` for generate pcl file from rosbag
## Installation
This repo is a ros workspace, containing several rospkgs:
* `interactive_tools` are customized tools to interact with gazebo and your robot
* `jackal_description` contains the modified jackal robot model descriptions
* `me5413_world` the main pkg containing the gazebo world, and the launch files
