# Unity-ROS-Basic-Simulation
Setting up the Unity Game Engine as a robotics simulator using Robot Operating System(ROS) and ROS#.</br>

## Overview:  
The [Unity Game Engine](https://unity.com/) is the world's most popular development platform for creating 2D and 3D multiplatform games.</br>
The platform is known for the highly accurate PhysX Engine and also the great user interface.</br>
These advantages can be used for setting up complex simulation environments fo robots. Robots can be extensively tested on a platform like Unity.
In this repository a simulation platform for robots was developed on the Unity Game Engine and essential features of a simulation environment were incorporated into the framework. A complete end to end framework of ROS and Unity was set-up to achieve this task.

## Goal:
This project sets up the motion of a simple differential drive robot in Unity and is controlled from the ROS side using teleoperation. 
1. Installation:</br>
    1. ROS-Melodic
    2. Unity3D
    3. rosbridge webserver
    4. ROS#
2. Communication between ROS and Unity is set-up using RosBridge webserver(on the ROS side) and Ros#(on the Unity side).
3. Essential sensor data i.e. the pose of the bot in Unity is communicated to ROS and is published on a topic.
4. Velocity commands on the _cmd_vel_ topic are subscribed on the Unity side and a control script ensures traversal of the bot with accordance to the subscribed commands.  

## Installation and Requirements:</br>
The set-up was done on a Ubuntu 18.04 system.</br>
ROS-melodic and Unity 2019.4.7 version were used.</br>
### Rosbridge webserver installation:
Rosbridge server facilitates communication on the ROS side.
Simply using sudo-apt
```sh
sudo apt-get install ros-<rosdistro>-rosbridge-server
```
For tutorials: http://wiki.ros.org/rosbridge_suite

### ROS# installation:
[ROS#](https://github.com/siemens/ros-sharp) are a set of tools that facilitate communication on the Unity side.</br>
ROS# can be installed using the Unity Asset Store in the Unity Project itself (Window->Asset Store) or by cloning the [ROS# repository](https://github.com/siemens/ros-sharp) in the Assets folder of the unity project.
```sh
git clone https://github.com/siemens/ros-sharp.git
```
## ROS-UNITY setup:
The commmunication is setup by launching rosbridge server.
```sh
roslaunch rosbridge_server rosbridge_websocket.launch
```
### Pose conversation:
The _Pose_Stamped_Publisher_ script of ROS# is used to send pose of the bot to ROS. The script is simply attached to the gameObject(The robot here) and some minor settings in the inspector and the script facilitates sending of pose to ROS.  
### Velocity conversation:
The velocity commands are accepted from the user using the turtlebot3 teleoperation package. 
```sh
export TURTLEBOT3_MODEL=waffle_pi
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
On the Unity side, _Twist_Subscriber_ script of the ROS# package subscribes to the incoming _Twist_ messages on _cmd_vel_. 
A control script written in C# (updown.cs) makes sure that the velocity commands recieved are converted to motion.

## Simulations:
Below are screen captures for the simulation. A similar simulation is also done in gazebo to point out that Unity has equal or maybe more capabilties than Gazebo for robot simulations.
### Unity Simulation:
https://user-images.githubusercontent.com/61026273/119505369-80dc7480-bd8a-11eb-900c-1826fd01f65e.mp4

The rqt_graph for the same:</br>
![rosgraph_unity](https://user-images.githubusercontent.com/61026273/119505620-c39e4c80-bd8a-11eb-84a9-e6fdd1410712.jpg)

### Gazebo Simulation:
https://user-images.githubusercontent.com/61026273/119505723-df095780-bd8a-11eb-8cc4-e50be0a9f49a.mp4

The rqt_graph for the same:</br>
![rosgraph_gazebo](https://user-images.githubusercontent.com/61026273/119505869-02cc9d80-bd8b-11eb-8c16-2e5b51f6e621.jpg)

## Files:
UnityROS is the complete Unity Project.
