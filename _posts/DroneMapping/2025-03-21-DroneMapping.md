---
layout: post
title:  "Drone Mapping with 2D LiDAR"
name:   "drone-mapping"
categories: [
    ROS2,
    LiDAR,
    Mapping,
    Drone
]
image: assets/posts/DroneMapping/thumbnail.mp4
featured: true
hidden: false
---

**Built for outdoor mapping, this drone is equipped with a 2D LiDAR and camera, giving it the power to map real-world environments by capturing and processing spatial data in real-time.**

<video autoplay loop controls muted src="{{ site.baseurl }}/assets/posts/DroneMapping/thumbnail.mp4" width="80%"></video>


### Introduction

This project was all about getting a drone to map the world around it using a 2D LiDAR and a camera. The idea was simple: take a drone, strap on some sensors, and make it capture its surroundings in real-time. Of course, in practice, that turned out to be way harder than expected. Between hardware quirks, unreliable network connections, and finicky data processing, there were plenty of challenges—but in the end, it worked! The drone successfully mapped real environments, and along the way, I got a solid crash course in drones, mapping, and making everything play nicely together.

### Why a 2D LiDAR instead of 3D?  

A 3D LiDAR was definitely an option, and it's commonly used for mapping applications. However, I wanted something simpler and more lightweight. A 2D LiDAR provided a good balance—it’s easier to integrate, requires less processing power, and still gives a useful overview of the surroundings. Given the outdoor conditions and network limitations, keeping things simple made the whole system more efficient and practical for real-time mapping.

### Overview  

<img src="{{ site.baseurl }}/assets/posts/DroneMapping/Diagram.png" width="60%">

*A block diagram of the components.*

#### 1. The Drone  

**Holybro X500 V2** – A solid, modular drone frame that’s great for research and tinkering.   

#### 2. The 2D LiDAR  

**Slamtech RPLiDAR C1** – Small, light (120g), and does the job well. Spins around and gives a full 360° 2D scan of the surroundings.  

#### 3. The Flight Controller  

**Holybro Pixhawk 6C** – The brains of the operation, running PX4 firmware to keep everything stable and feed odometry data to the mapping pipeline.  

#### 4. ROS Packages  

This whole thing runs on ROS2, with a mix of existing and custom packages:  

* **sllidar_ros2** ([Link](https://github.com/Slamtec/sllidar_ros2)) – Pulls scan data from the LiDAR and publishes it to `/scan`.  
* **px4_msgs** ([Link](https://github.com/PX4/px4_msgs)) – Interfaces with the Pixhawk for flight data like IMU and GPS readings.  
* **px4_odometry_converter** – Converts PX4’s odometry format into a standard ROS2 `/odom` message.  
* **laser_tf_publisher** – Handles the necessary transformations between different coordinate frames.  
* **cartographer** ([Link](https://github.com/cartographer-project/cartographer_ros)) – Takes all the sensor data and builds an occupancy grid map.  

### 5. Mechanical Setup  

Everything was mounted on the drone with stability in mind. The LiDAR sat on top for an unobstructed 360° scan, while the Pixhawk was placed lower for easy access. A POV camera was also added to record flights and review what the drone was seeing during mapping.  

<img src="{{ site.baseurl }}/assets/posts/DroneMapping/assm-drone-bg.png" width="60%">  

*The drone’s mechanical setup.*

### The Results  

After some rough early tests (with plenty of drifting and data drops), things finally started coming together. A portable router made a huge difference in improving network stability, allowing for much better outdoor mapping. The drone successfully mapped places like Shakespeare Garden and Howes Chapel, capturing a solid representation of the environment. I mapped [Howes Chapel](https://maps.app.goo.gl/XwsJKi22oduVkMoc8), a spot I really enjoy spending time in. Once I dialed in the right mapping parameters (thank you, ROS bag) the system became pretty reliable. Now, as long as the drone can fly safely, it can map just about anywhere.

<img src="{{ site.baseurl }}/assets/posts/DroneMapping/full-building.png" width="60%">  

*The complete map real of Howes Chapel.*

<iframe width="560" height="315" src="https://www.youtube.com/embed/BWT-F1g8_w0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

*The complete video for the map above.*

### Takeaways and Conclusions  

This project was a wild ride. Some key lessons:  

- **Hardware always takes more time than expected.** Mounting, wiring, and debugging took way longer than I thought.  
- **Network issues will mess up everything.** Using a phone hotspot was a bad idea—switching to a portable router fixed a lot of problems.  
- **Real-world mapping isn’t as clean as simulations.** Outdoor conditions, sensor noise, and unexpected issues made everything trickier than in a controlled test, and overcoming those challenges was a key part of this project.
- **Future upgrades** could include better GPS integration for more accuracy and trying multi-drone mapping (if I can get the time and approvals to fly more than one).  

Despite all the hurdles, this was a super rewarding project. The final mapping results turned out great, and the hands-on experience with drones and real-world mapping was invaluable!  
