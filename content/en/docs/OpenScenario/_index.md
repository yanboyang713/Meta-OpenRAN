---
title: "Open Scenario"
linkTitle: "OpenScenario"
weight: 1
description: >
  Open Scenario
---

{{% pageinfo %}}
This is page for Open Scenario
{{% /pageinfo %}}

# Overview
![](https://res.cloudinary.com/dkvj6mo4c/image/upload/v1672096805/Open_Scenario_zskcmw.png)

# Components
+ Network Simulator: NS3
+ UAV Physical Simlator: AirSim + Gazebo
+ Co-Simulator: FlyNetSim
+ Ground Control Stations: QGroundControl + MAVProxy

# setup ArduPilot SITL
https://ardupilot.org/dev/docs/building-the-code.html#building-the-code

# Set-up AirSim + Gazebo
https://microsoft.github.io/AirSim/

https://microsoft.github.io/AirSim/docker_ubuntu/

# Set-up QGroundControl + MAVProxy
http://qgroundcontrol.com/
https://ardupilot.org/mavproxy/

# Create Scenario
Includes:
+ Captive Balloon
+ Fixed-wing Drone
+ Quadcopter Drone

# Set-up FlyNetSim with NS3
https://github.com/saburhb/FlyNetSim

# Reference List
Baidya, S., Shaikh, Z. and Levorato, M., 2018, October. FlyNetSim: An open source synchronized UAV network simulator based on ns-3 and ardupilot. In Proceedings of the 21st ACM International Conference on Modeling, Analysis and Simulation of Wireless and Mobile Systems (pp. 37-45).

Gill, J.S., Velashani, M.S., Wolf, J., Kenney, J., Manesh, M.R. and Kaabouch, N., 2021, May. Simulation Testbeds and Frameworks for UAV Performance Evaluation. In 2021 IEEE International Conference on Electro Information Technology (EIT) (pp. 335-341). IEEE.

Network simulators are software that helps analyze and predict the behavior of a particular configuration such as UAV communications before implementing it into the real world.

# UAV NETWORK SIMULATORS
## NS3
NS3 only supports two-dimensional visualization using PyViz and NetAnim. PyViz supports live simulation visualization, which means it does not use trace files. PyVis is mostly written in Python, but it supports both C++ and python simulations. Contrary to PyViz, NetAnim is an offline simulator developed using the Qt toolkit. NetAnim uses XML trace files collected during simulation. It supports Flying AdHoc Network (FANET) routing protocols like AODV, DSDV, and DSR. Due to the lack of good three-dimensional mobility models, NS3 cannot be recommended for research where threedimensional mobility is crucial for accurate results.

## OMNET++
OMNET++ is a modular, extensible, component-based network simulator based on a C++ framework. It is an opensource software primarily used for network simulations. OMNET++ is not a simulator by itself, it is a network simulation platform used by a large group of people for both research and commercial purposes. Components (models) of OMNET++ are written in C++ and put together into larger components with the use of high-level language (NED). The highly modular nature of the components makes OMNET++ models easily reusable. The development environment is based on the Eclipse platform. OMNET++ supports a Command-line interface (Cmdenv) for simulation interface and a Qtenv based interactive runtime simulation GUI [11]. It has good documentation and some sample simulations to get started. OMNET++ can run on all platforms that have a C++ compiler as the simulation kernel is standard C++. The simulation IDE supports Linux, macOS, and Windows. 

# UAV PHYSICAL SIMULATORS
physical simulations of real-world environments offer the ability to be able to gather environment-based training data from which different actors can learn (actors can vary from fixed-wing or multirotor UAVs to cars). Sensor models such as Lidar and GPS provide data feedback that can be closely related to the real world, while actor models can allow for computer vision development. UAV Physics simulation environments take advantage of different “gaming engines” that offer high graphical fidelity that closely resembles the real world.

A non-exhaustive list of motion capture software includes Microsoft AirSim, MatLab UAV Toolbox, Gazebo, and JMavSim

## AirSim
AirSim is an open-source vehicle simulation that is built on the Unreal Engine platform [18]. AirSim is a product of the Microsoft Research and Development division.
AirSim has a variety of sensors that can be implemented into the drone simulation. These sensors range from Barometer, Lidar, GPS, IMU Gyroscope, Accelerometer, and Collision Detection. AirSim also simulates the MavLink protocol. AirSim offers hi-fidelity physical and visual simulation to generate a large quantity of training data cheaply for building machine learning models [18]. AirSim offers a robust platform to implement AI/ML algorithms and run learning experiments for UAVs. 

## Gazebo
Gazebo is a very popular simulation tool that is widely used in the robotics community. Like AirSim, Gazebo enables the researcher to test algorithms and build an Artificial Intelligence/Machine Learning platform for a wide variety of robotics applications. Gazebo uses different physics engines such as ODE to create various dynamics simulations [20]. In addition to physics engines, Gazebo uses OGRE, a gaming engine, to provide advanced simulation environment graphics and a higher level of accuracy of training data. OGRE is a graphics creation environment tool that the researcher can use to create and alter different testing environments.

Gazebo can connect to a robot control framework known as a ROS.

# DISTRIBUTED Co-SIMULATORS AND FRAMEWORKS
## FlyNetSim
FlyNetSim uses Ardupilot for physical simulator and NS-3 as a network simulator. [23] were able to execute a real-time simulation of 40 drones, which consumed about 50% of the CPU. It uses a lightweight custom-built middleware for UAV network simulation. It also supports emulation of UAVs. It has the potential to grow but is not regularly maintained by the developers. 

# GROUND CONTROL STATIONS SOFTWARE
## MISSION PLANNER
Mission planner is a GCS for copters, planes, and Rovers. It is open-source, community-supported software that supports ArduPilot open-source projects. It has good documentation and regular development support, which makes it easy to use and understand. It is developed in Python programming language by Michael Oborne. It is compatible with Google maps and also other maps for navigation [30].

## QGROUNDCONTROL
QGroundControl is a GCS that provides support for multiple vehicles and firmware type. It is an open-source software developed by Lorenz Meier [31]. It is written in C++ and based on Qt libraries. It supports Windows, macOS, Linux, Android, and iOS devices. It is configured explicitly for PX4 Pro and ArduPilot based vehicles. It also helps to manage multiple vehicles at a time. It allows the users to analyze MAVLink protocol messages, but not on the packet level. Moreover, it facilitates creating a mission for autonomous flights that can be visualized in a two-dimensional map on an in-built graphical interface.

## MAVPROXY
MAVProxy is an open-source GCS software for systems based on MAVLink, first developed by CanberraUAV [33]. It is a light, portable, and extendable GCS that can be run on almost all operating systems that support Python. It has a twodimensional visualization environment that can show UAV’s current position and waypoints [34]. It can be complemented with other GCS station tools, such as Mission planner and QGroundControl. Some studies used MAVproxy to implement attacks on the UAV system to indicate vulnerabilities and gaps in mavlink protocol [35].


Stornig, A., Fakhreddine, A., Hellwagner, H., Popovski, P. and Bettstetter, C., 2021, April. Video Quality and Latency for UAV Teleoperation over LTE: A Study with ns3. In 2021 IEEE 93rd Vehicular Technology Conference (VTC2021-Spring) (pp. 1-7). IEEE.
