---
layout: post
title:  "Wheeled Robot Navigating a Maze"
categories: [
    Mechatronics,
    Microcontrollers,
    Arduino,
]
image: assets/posts/MazNavRobot/thumbnail.mp4
featured: true
hidden: false
---

**Wheeled robot navigating a maze using simple sensors, following the right hand wall.**

<video autoplay loop controls src="{{ site.baseurl }}/assets/posts/MazNavRobot/thumbnail.mp4" width="80%"></video>

The goal of this project was to make the wheeled robot shown above to solve any given maze, using sensors.

### The Hardware

The sensors provided were fairly limited, and are as follows:

- **Ultrasonic distance sensor** - one unit.
- **Distance sensor 2** - IR units.
- **TOF distance sensor** - one unit.
- **DOF 9 IMU component** - one unit.

The sensors were tactically positioned on the robot to in order to be able to navigate, each sensor was put in the respective direction (front, back left and right).


### The Code Block Diagram

The algorithm was adapted from the somewhat classic algorithm that follows a right hand wall. It is as follows (ChatGPT: fill the algoritm)
This algorithm however is suited for virtual environment and not for the real world. Adjustment were made for this alogrithm to increase its robustness, as shown in the figure below.

<img src="{{ site.baseurl }}/assets/posts/MazNavRobot/flowchart-bg.png" width="80%"/>

*Figure 1: The code block diagram.*

This block diagram has two key features: One , is the rotate left rule, as in sometimes the robot would be placed such there is no right wall near it. The second is that adding the rotate to the left also could lock the robot to go back and forth rotating left and right, so the code also checks if such thing happened too much (5 times) and then moves it a little bit in order to circumvent this.

### The Implementation

The main controller was an Arduino Uno, to which a DC motor controller board and the sensors (see `The Hardware`) and the algorithm described above was implemented. The raw data from the sensors was converted to a boolean statements, for example if the distance was lower than a certian thereshold, then it would be considered that the robot has something to the side in which the sensor was mounted.


<br><br>

### Acknowledgments

This was a group project, as a part of a competiton that was held to solve a larger maze, which was not fully described here. The team members were:

Guy Appel, Omri Dalin, Or Dallal, Rani Linkov, Meital Valach
