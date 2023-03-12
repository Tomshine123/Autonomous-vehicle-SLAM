# My_project
This repository is my implementation for ME5413 Autonomous Mobile Robotics Final Project
>Main Author: Zhang Ceng

![Ubuntu 20.04](https://img.shields.io/badge/OS-Ubuntu_20.04-informational?style=flat&logo=ubuntu&logoColor=white&color=2bbc8a)
![ROS Noetic](https://img.shields.io/badge/Tools-ROS_Noetic-informational?style=flat&logo=ROS&logoColor=white&color=2bbc8a)
![C++](https://img.shields.io/badge/Code-C++-informational?style=flat&logo=c%2B%2B&logoColor=white&color=2bbc8a)
![Python](https://img.shields.io/badge/Code-Python-informational?style=flat&logo=Python&logoColor=white&color=2bbc8a)

## Dependencies
The requirement can be found in https://github.com/NUS-Advanced-Robotics-Centre/ME5413_Final_Project and also an extra ros package
  * `pcl_ros` is used for generate pcl file from rosbag
## Installation
This repo is a ros workspace, containing several rospkgs:
* `ALOAM` is SLAM algorithm package used for 3D mapping
* `costmap_prohibition_layer` provides a plugin to add virtual obstacle in costmap to set prohibited region
* `interactive_tools` are customized tools to interact with gazebo and your robot
* `jackal_description` contains the modified jackal robot model descriptions
* `jackal_navigation` contains a probabilistic localization system for navigation
* `me5413_world` the main pkg containing the gazebo world, and the launch files
* `pcd2pgm` for converting pcd file to pgm map which can be used for navigation
```bash
# Clone this repo
cd
git clone https://github.com/Tomshine123/My_project.git
cd My_project

# Install all dependencies
rosdep install --from-paths src --ignore-src -r -y

# Build
catkin_make
# Source 
source devel/setup.bash
```
To properly load the gazebo world, you will need to have the necessary model files in the `~/.gazebo/models/` directory, which installation instructions can be found in URL above.
## Usage
### 1. Mapping
Following commands will launch the gazebo with the project world and also A-LOAM SLAM for 3D Lidar
```bash
# Launch Gazebo World together with our robot
roslaunch me5413_world world.launch
```
In the second terminal, launch A-LOAM SLAM for 3D Lidar
```
roslaunch aloam_velodyne aloam_velodyne_VLP_16.launch 
```
In order to drive the robot around for mapping, launch keyboard control node in the third terminal
```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py 
```
By above you can visualize pointclouds, and finish mapping by exploring all possible areas
![pointcloud](src/me5413_world/media/pointcloud.png)
To save the pointclouds in a pcl file, run rosnode in `pcl_ros` package to generate file in current direction
```
rosrun pcl_ros pointcloud_to_pcd input:=/laser_cloud_surround
```
![pc_map](src/me5413_world/media/pc_map.png)
To convert the pcl file to pgm format, run rosnode in `pcd2pgm` package after modify the path in `test.cpp`
```
private_nh.param("file_directory", file_directory, std::string("/home/tommy/pcd/")); # the path to pcd file
```
```
private_nh.param("file_name", file_name, std::string("12673.944000000")); # the name of the pcd file
```
After transforming you can obtain the global map by 3D Lidar SLAM like below and also a corresponding .yaml file and put them into `src/me5413_world/maps/`

![map](src/me5413_world/media/map.png)
### 2. Navigation
To begin with adding prohibited region in the map, create `prohibition_areas.yaml` in `My_project/src/jackal_navigation/params/map_nav_params/` and add the following content to the file
```bash
prohibition_areas:

# define an obstacle point
# - [17.09, -6.388]
 
# define  an obstacle line
 - [[4.5, 1.5],
    [4.5, 5.0]]
 - [[1.0, 1.0],
    [3.0, 1.0]]

# define  an obstacle region
#- [[-11.15, -15.614],
#   [-12.35, -13.89],
#   [-10.05, -12.218]]
```
Close all terminals and start new one in the workspace
```bash
source develop/setup.bash
roslaunch me5413_world world.launch
```
In the second terminal launch the navigation node
```bash
roslaunch me5413_world navigation.launch
```
Click the buttons of the bottom right panel in rviz and navigation to the specified pose
![navigation](src/me5413_world/media/navigation.png)

## Support

If you have any questions please feel free to open a pull-request

## License

The [My_Project](https://github.com/Tomshine123/My_project) is released under the [MIT License](https://github.com/Tomshine123/My_project/blob/main/LICENSE)
