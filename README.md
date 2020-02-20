# Introduction
<p align="justify">

This lesson is all about the Robot Operating System or ROS for short. ROS is widely used across the industry and academia for building robotics applications. ROS is an Open Source Robotics framework that provides libraries and tools for working with hardware and for passing messages between components. ROS also has tools for visualization, simulation and analysis as well as extensive community support and an interface to numerous powerful software libraries. 

# Brief History of ROS

Development of ROS began in the mid-2000s as Project Switchyard in Stanford's Artificial Intelligence Laboratory. In 2007, ROS became a formal entity with support from Willow Garage. Since 2013, the Open Source Robotics Foundation has been maintaining and developing ROS.
<p align="center">
<img src="./img/1.png" alt="Brief History of ROS" />
<p align="center">
  
One of the primary motivations for developing ROS was the recognition that researchers were constantly reinventing the wheel where there were not many reusable robotics software components that could be used as a starting point for a project. In addition, because different groups were all working on custom solutions, it was difficult for them to share code and ideas, It was also difficult to compare results. ROS aims to facilitate the development process by eliminating these problems.

<p align="center">
<img src="./img/2.png" alt="Brief History of ROS" />
<p align="center">
  
Lots of people and lots of companies use ROS. There are drones, kinematic arms, wheeled robots and even bipedal robots out there using ROS, every day.

# Nodes and Topics

Pretty much all the robots share the same basic characteristics of containing sensors for perceiving the world around them, software for making high level decisions and motors and controllers for actuation. ROS provides a powerful communications system allowing these different components (perception, decision making and actuation components) to communicate with one another by considering a generic robot. This robot could be a drone, a mobile base or even a robotic arm. While these robots may be composed of very different physical components, they are all built to perform these same three high level steps of perception, decision making and actuation.

<p align="center">
<img src="./img/3.png" alt="Nodes and Topics" />
<p align="center">
  
On the software side, ROS manages these three complex steps by breaking each of them down into many small unit processes called nodes. Typically, each node on the system is responsible for one small and relatively specific portion of the robot's overall functionality.

<p align="center">
<img src="./img/4.png" alt="Nodes and Topics" />
<p align="center">
  
For example, there may be nodes for each sensor and actuator in the system as well as nodes for things like position estimation, behavior execution and motor control (See above).

At the center of the collection of nodes is the ROS Master, which acts as a sort of manager of all the nodes. The ROS Master maintains a registry of all the active nodes on a system and then allows each node to discover other nodes in the system and establish lines of communication with them. 

Note: The ROS master allows nodes to locate one another but after that they connect with each other directly.
In addition to allowing nodes to locate one another and communicate, the ROS Master also hosts what has called the parameter server. As its name suggests, the parameter server is typically used to store parameters and configuration values that are shared amongst the running nodes. For example, a mobile robot's wheel radius may be used by one node to estimate position and by another to calculate speed and rather than storing the same information in multiple places, nodes can look up values as needed(See below).

  

</p>
