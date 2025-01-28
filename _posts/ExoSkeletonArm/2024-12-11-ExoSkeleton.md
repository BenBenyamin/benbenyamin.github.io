---
layout: post
title:  "Arm Assistive Exoskeleton"
categories: [
    SolidWorks,
    CAD,
    Mechatronics,
    Arduino,
    FEA
]
image: assets/posts/ExoSkeletonArm/thumbnail.mp4
featured: true
hidden: false
---

**The arm assistive exoskeleton is worn on the arm and forearm, providing assistive force to help with lifting, reaching, grasping, holding, and carrying. It is designed for individuals with muscle weakness from peripheral neurological conditions, such as traumatic or neuropathic injuries, which cause upper limb dysfunction..**

<video autoplay loop controls src="{{ site.baseurl }}/assets/posts/ExoSkeletonArm/thumbnail.mp4" width="80%"></video>

### Introduction

People with muscle weakness from peripheral neurological conditions often experience temporary functional decline. Such people could include, for example, stroke survivors,people with traumatic injuries and more. Basic tasks such as grocery shopping, opening bottles, and lifting objects may become difficult or even impossible, leading to a decrease in their quality of life. The Arm Assistive Exoskeleton was created to assist these individuals in performing such tasks, aiding their recovery (by motivating them to move their arm) and improving their quality of life, making everyday activities more manageable.

The objective was of this project was to design a system that allows the user to regain basic functionality back in their less functional hand . The requirements were defined to be grasping and lifting of an item with a diameter/width ranging from 0 to 100 mm and a maximum lifting weight of 1 kg. All while weighing around 1.3 kg, in order not to encumber the user too much. 

A prototype was manufactured as a proof of concept.

### Overview

<img src = "{{ site.baseurl }}/assets/posts/ExoSkeletonArm/overview.png" width="50%">

*Overview of exoskeleton arm*


#### 1. The Arm Attachment

                
<img src = "{{ site.baseurl }}/assets/posts/ExoSkeletonArm/flex-detailed.png" width="80%">

*A detailed look on the arm attachment and the flex mechanism*

his is the part worn by the user. The frame components, designed to rest on the arm, feature a foam core for comfort and a carbon fiber outer shell for strength. A DC motor is mounted on the upper arm and connected to the forearm by a timing belt. When the motor spins, it drives the movement of the arm, assisting the user in flexing their arm.

#### 2. The Gripper

<img src = "{{ site.baseurl }}/assets/posts/ExoSkeletonArm/gripper-detailed.png.png" width="80%">

*A detailed look on the arm attachment and the gripping mechanism*

Since the user has lost some strength in their arm, simply flexing it isn't enough—gripping objects is also essential. To address this, the gripper was designed. It is a parallel gripper, meaning its jaws remain parallel to each other as they open and close. The gripper is controlled by a special glove worn by the user, allowing them to control the gripper to grasp objects.

### The Design Process

The mechanical parts were design in SolidWorks, and for the prototype, manufactured in a variety of methods such as CNC milling, laser cutting, and 3D printing. The control was done with an Arduino Uno.

### Structural Analysis

In order to know what kind of motor to use, a structural analysis was done. The assumption is that the system is slow enough that it is most of the time in equilibrium.

#### 1. The Arm Attachment


<img src = "{{ site.baseurl }}/assets/posts/PointNet/PointNet.png" width="80%">

*free body diagram-me.*


