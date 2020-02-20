# 1. Introduction
<p align="justify">

This lesson is all about the Robot Operating System or ROS for short. ROS is widely used across the industry and academia for building robotics applications. ROS is an Open Source Robotics framework that provides libraries and tools for working with hardware and for passing messages between components. ROS also has tools for visualization, simulation and analysis as well as extensive community support and an interface to numerous powerful software libraries. 

# 2. Brief History of ROS

Development of ROS began in the mid-2000s as Project Switchyard in Stanford's Artificial Intelligence Laboratory. In 2007, ROS became a formal entity with support from Willow Garage. Since 2013, the Open Source Robotics Foundation has been maintaining and developing ROS.
<p align="center">
<img src="./img/1.png" alt="Brief History of ROS" />
<p align="center">
  
One of the primary motivations for developing ROS was the recognition that researchers were constantly reinventing the wheel where there were not many reusable robotics software components that could be used as a starting point for a project. In addition, because different groups were all working on custom solutions, it was difficult for them to share code and ideas, It was also difficult to compare results. ROS aims to facilitate the development process by eliminating these problems.

<p align="center">
<img src="./img/2.png" alt="Brief History of ROS" />
<p align="center">
  
Lots of people and lots of companies use ROS. There are drones, kinematic arms, wheeled robots and even bipedal robots out there using ROS, every day.

# 3. Nodes and Topics

Pretty much all the robots share the same basic characteristics of containing sensors for perceiving the world around them, software for making high level decisions and motors and controllers for actuation. ROS provides a powerful communications system allowing these different components (perception, decision making and actuation components) to communicate with one another by considering a generic robot. This robot could be a drone, a mobile base or even a robotic arm. While these robots may be composed of very different physical components, they are all built to perform these same three high level steps of perception, decision making and actuation.

<p align="right">
<img src="./img/3.png" alt="Nodes and Topics" width="600" height="400"/>
<p align="right">
  
On the software side, ROS manages these three complex steps by breaking each of them down into many small unit processes called nodes. Typically, each node on the system is responsible for one small and relatively specific portion of the robot's overall functionality.

<p align="right">
<img src="./img/4.png" alt="Nodes and Topics" width="600" height="400" />
<p align="right">
  
For example, there may be nodes for each sensor and actuator in the system as well as nodes for things like position estimation, behavior execution and motor control (See above).

At the center of the collection of nodes is the ROS Master, which acts as a sort of manager of all the nodes. The ROS Master maintains a registry of all the active nodes on a system and then allows each node to discover other nodes in the system and establish lines of communication with them. 

Note: The ROS master allows nodes to locate one another but after that they connect with each other directly.
In addition to allowing nodes to locate one another and communicate, the ROS Master also hosts what has called the parameter server. As its name suggests, the parameter server is typically used to store parameters and configuration values that are shared amongst the running nodes. For example, a mobile robot's wheel radius may be used by one node to estimate position and by another to calculate speed and rather than storing the same information in multiple places, nodes can look up values as needed(See below).

<p align="right">
<img src="./img/5.png" alt="Nodes and Topics" width="600" height="400"/>
<p align="right">
 
Nodes can share data with one another by passing messages over what are called topics. A topic is simply a named bus which you can think of as a pipe between nodes through which messages flow. 

In order to send a message on a topic, we say that a node must publish to it. Likewise, to receive a message on a topic, a node must subscribe to it. Below is an example of the topics called publish subscribe or a pub sub architecture (the arrows represent message flow from publishers to subscribers).


<p align="right">
<img src="./img/6.png" alt="Nodes and Topics" width="600" height="400"/>
<p align="right">

It's important to note that each node may simultaneously publish and subscribe to a wide variety of topics.

# 4. Message Passing Types

Each ROS distribution comes with a wide variety of predefined message types which are available for your use. There are message types for communicating physical quantities, such as positions, velocities, accelerations, rotations and durations. There are also messages for communicating sensor readings such as laser scans, images, point clouds, inertial measurements and more.

The number of message types available in a full ROS install is actually quite staggering and you can to define your own type.
It's important to note that although the named messages would seem to imply text based contents, they can in fact contain any kind of data. Below is an example of the message types associated with the topics we looked at earlier.

<p align="right">
<img src="./img/7.png" alt="Message Passing Types" width="600" height="400"/>
<p align="right">
  
In the above case, the topic called camera_images is transporting image messages from the camera node to the position estimator node and so on.

# 5. Services

Passing messages over topics between publishers and subscribers is useful but it's not a one size fits all communications solution. There are times when a request response pattern is useful. For these types of interactions, ROS provides what are called services.
Like topics, services allow the passing of messages between nodes. However, unlike topics, a service is not a bus and there are no publishers or subscribers associated with them. Instead, nodes interacting via services do on a one to one basis (1-1) using a request and response messages.

Let's take a look at how a service might be used in an example. Let's say that the behavior executor node wants to capture an image from the camera. We could just have it subscribe to the camera images topic. It would then receive a new image each time the camera node publishes one (See below).


<p align="right">
<img src="./img/8.png" alt="Services" width="600" height="200" />
<p align="right">

The request message definition might be a custom message type called exposure time and the response might just be an image message. By issuing a service call to the capture_image service, the behavior executor node is able to request the camera should capture an image with a given exposure time setting (2 milisecond). The camera node will then respond to the request by sending a message containing the resulting image.

<p align="right">
<img src="./img/1.gif" alt="Services" width="600" height="200" />
<p align="right">
  
  
  
  
</p>
