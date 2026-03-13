# ROS 2 Differential Drive Robot with Potential Field Navigation

## Overview

This project demonstrates how a mobile robot can **navigate toward a goal while avoiding obstacles** using the **Potential Field Method**.

The system is implemented as a **ROS 2 simulation** of a differential drive robot equipped with a **LiDAR sensor** in Gazebo.

The robot continuously analyzes its surroundings and adjusts its motion so that it:

* moves toward a target location
* avoids obstacles detected by its LiDAR sensor
* produces smooth navigation behavior in real time

The goal of this project is to provide a **clear, educational example of how classical robot navigation algorithms work** when implemented in a modern robotics framework.

---

# How the System Works (Conceptual Explanation)

Robot navigation in this project is based on the **Potential Field Method**, a concept inspired by physics.

The idea is simple:

### 1. The goal attracts the robot

The destination generates an **attractive force** that pulls the robot toward it.

The farther the robot is from the goal, the stronger this attraction becomes.

### 2. Obstacles repel the robot

Each obstacle generates a **repulsive force**.

When the robot gets too close to an obstacle, this force pushes it away.

### 3. The robot follows the combined force

The robot calculates the **sum of all forces** acting on it.

This resulting force determines:

* the direction the robot should move
* how fast it should move
* how it should turn

By continuously updating this calculation using LiDAR data, the robot can navigate safely through an environment.

---

# Project Components

This repository contains three main parts.

## 1. Mathematical Model

The mathematical derivation of the potential field method used in this project is provided in:

```
docs/math_derivation_potential_field.pdf
```

The document explains:

* attractive potential fields
* repulsive potential fields
* force calculations
* how forces are converted into robot velocity commands

---

## 2. Robot Simulation Model

The robot is described using **URDF/Xacro**, which defines:

* the robot geometry
* the differential drive wheels
* the LiDAR sensor
* physical properties used in simulation

Files are located in:

```
ros2_ws/src/potential_field_robot/urdf/
```

The robot is simulated in **Gazebo**, where it interacts with obstacles in a virtual environment.

---

## 3. Navigation Controller

The main controller is implemented in Python as a ROS 2 node.

Its responsibilities include:

1. Reading LiDAR sensor data
2. Detecting nearby obstacles
3. Computing attractive and repulsive forces
4. Combining these forces into a motion command
5. Publishing velocity commands to move the robot

Controller file:

```
ros2_ws/src/potential_field_robot/scripts/potential_field_controller.py
```

---

# Repository Structure

```
ros2-potential-field-robot/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── docs/
│   ├── math_derivation_potential_field.pdf
│   ├── system_overview.pdf
│   └── implementation_notes.pdf
│
├── images/
│   ├── robot_model.png
│   ├── gazebo_simulation.png
│   ├── potential_field_diagram.png
│   └── lidar_scan_visualization.png
│
├── ros2_ws/
│   └── src/
│       └── potential_field_robot/
│           │
│           ├── launch/
│           │   └── simulation.launch.py
│           │
│           ├── urdf/
│           │   ├── robot.urdf.xacro
│           │   └── materials.xacro
│           │
│           ├── config/
│           │   └── lidar_params.yaml
│           │
│           ├── worlds/
│           │   └── obstacle_world.world
│           │
│           ├── scripts/
│           │   └── potential_field_controller.py
│           │
│           ├── package.xml
│           └── CMakeLists.txt
│
└── videos/
    └── simulation_demo.mp4
```

---

# Running the Simulation

## Prerequisites

You will need:

* ROS 2
* Gazebo
* Python 3

## Steps

Clone the repository and build the workspace:

```
cd ros2_ws
colcon build
source install/setup.bash
```

Launch the simulation:

```
ros2 launch potential_field_robot simulation.launch.py
```

This will:

1. Launch the Gazebo environment
2. Spawn the robot
3. Start the navigation controller

---

# Example Simulation

Screenshots and demonstrations can be found in the `images` and `videos` folders.

Example images:

```
images/gazebo_simulation.png
images/potential_field_diagram.png
```

---

# Educational Purpose

This project is intended as a **learning resource** for students and robotics enthusiasts who want to understand:

* robot navigation algorithms
* LiDAR-based obstacle avoidance
* ROS 2 robotics software architecture
* differential drive robot control

The code and documentation aim to make these ideas **accessible even to readers with limited robotics background**.

---

# Future Improvements

Possible extensions include:

* dynamic obstacle handling
* improved path planning algorithms
* comparison with other planners such as A* or RRT
* deployment on a real robot platform
* integration with additional sensors

---

# License

Specify your license here (MIT License is commonly used for educational and research projects).

---

# Acknowledgments

This project was developed as part of a learning exploration into mobile robot navigation, combining theoretical modeling with practical ROS 2 simulation.

Contributions, suggestions, and improvements are welcome.

