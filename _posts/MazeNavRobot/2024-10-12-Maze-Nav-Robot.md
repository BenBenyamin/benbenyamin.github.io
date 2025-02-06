---
layout: post
title:  "Wheeled Robot Navigating a Maze"
name : "maze"
categories: [
    Mechatronics,
    Microcontrollers,
    Arduino,
]
image: assets/posts/MazNavRobot/thumbnail.mp4
featured: true
hidden: false
---

**Wheeled robot navigating a maze using simple sensors, following the right-hand wall.**

<video autoplay loop controls src="{{ site.baseurl }}/assets/posts/MazNavRobot/thumbnail.mp4" width="80%"></video>

The goal of this project was to make the wheeled robot shown above solve any given maze using sensors.

### The Hardware

The sensors provided were fairly limited, and are as follows:

- **Ultrasonic distance sensor** - one unit.
- **Distance sensor 2** - IR units.
- **TOF distance sensor** - one unit.
- **DOF 9 IMU component** - one unit.

The sensors were tactically positioned on the robot to enable navigation. Each sensor was placed in the respective direction (front, back, left, and right).

### The Code Block Diagram

The algorithm was adapted from the somewhat classic algorithm that follows a right-hand wall. It is as follows (ChatGPT: fill the algorithm).

This algorithm, however, is suited for virtual environments and not the real world. Adjustments were made to increase its robustness, as shown in the figure below.

<img src="{{ site.baseurl }}/assets/posts/MazNavRobot/flowchart-bg.png" width="80%"/>

*Figure 1: The code block diagram.*

This block diagram has two key features:
1. The **rotate left** rule: Sometimes the robot would be placed in a way that there was no right wall near it.
2. Adding the **rotate left** rule could cause the robot to get stuck, rotating back and forth. Therefore, the code checks for this scenario (if it happens more than 5 times) and moves the robot slightly to circumvent it.

### The Implementation

The main controller was an Arduino Uno, to which a DC motor controller board and the sensors (as detailed in *The Hardware*) were connected. The algorithm described above was implemented on this setup. The raw data from the sensors was converted into boolean statements. For example, if the distance was lower than a certain threshold, it would be considered that the robot has something beside it in the direction of the mounted sensor.

<br><br>

### Acknowledgments

This was a group project as part of a competition to solve a larger maze, which was not fully described here. The team members were:
Guy Appel, Omri Dalin, Or Dallal, Rani Linkov, Meital Valach
