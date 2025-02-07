---
layout: post
title:  "Path Finding in a 2D Environment for a Robot"
name:   "pathfinding"
categories: [
    Python,

]
image: assets/posts/Pathfinding/thumbnail.mp4
featured: true
hidden: false
---

**Pathfinding is crucial for robot navigation, allowing robots to move through their environment. In this project, A* algorithm was used to help a robot navigate obstacles and reach its goal while considering its size.**

<video autoplay loop controls src="{{ site.baseurl }}/assets/posts/Pathfinding/thumbnail.mp4" width="80%"></video>

### Task Overview

The goal was to help a 2D robot navigate an obstacle course. The robot needed to reach a target within an environment filled with obstacles while factoring in its size.

The obstacle course was manually mapped by recording the coordinates of each obstacle relative to a reference point (x0, y0). For circular obstacles, the center coordinates were noted, while complex shapes were broken down into smaller rectangular obstacles.

For example, the 'L' shape in the bottom-left corner was represented by two rectangles: one with a width of 11.5 meters and height of 1 meter, and the other with a width of 1 meter and height of 5.5 meters, as shown in Figure 1.

<img src="{{ site.baseurl }}/assets/posts/Pathfinding/obstacles.png" width="80%"/>

*Figure 1 - Mapping the Obstacle Space*

## Defining Obstacle Objects

To enable path planning, two obstacle objects were created: `RoundObstacle` and `RectangleObstacle`, implemented in the attached `Obstacle.py` file. Both inherit from the `Obstacle` object. The `RoundObstacle` contains the center's location and radius, while the `RectangleObstacle` includes height, width, and the bottom-left corner coordinates. Each object features the following functions:

1. **`isColliding(self, point)`** – Checks if a point collides with the obstacle.
2. **`isLineColliding(self, line)`** – Checks if a line intersects with the obstacle.
3. **`plot(self, **kwargs)`** – Plots the object using `matplotlib`.

The `Line` object calculates the line's slope and length and includes functions for calculating its value at specific points and checking if a point lies on the line.

To account for the robot’s radius, obstacles are "inflated" by this radius. Circular obstacles have their radius increased, while rectangular obstacles have each side extended with the robot’s radius, and corners are rounded using circular obstacles, resulting in a shape resembling a rectangle with rounded corners.

<img src="{{ site.baseurl }}/assets/posts/Pathfinding/inflate.png" width="80%"/>

*Figure 2: Top - Rectangular Obstacle, Bottom - "Inflated" Rectangular Obstacle*

An `InflatedRectangleObstacle` object is a list of 5 `RectangleObstacle` (the center and sides with the robot’s radius) and 4 `RoundObstacle` at the corners. It uses the same collision-checking functions as the individual obstacles. The main file creates lists of both the regular and inflated obstacles, with the `isColl(point)` and `isLineColl(line)` functions checking for collisions against the inflated obstacles.

<img src="{{ site.baseurl }}/assets/posts/Pathfinding/inflated_obst.png" width="80%"/>

*Figure 3: Left - Obstacle Map, Right - Inflated Obstacle Map*

## Calculating the Shortest Path with the A* Algorithm

To find the shortest path between the start and end points, the A* algorithm was used. This algorithm guarantees finding the shortest path between two nodes in a graph. Since the given map is continuous, it was discretized into points forming a graph—where the nodes are the points, and the edges are the connections to adjacent points. The pseudocode for A* can be found here: [A* Search Algorithm Pseudocode](https://en.wikipedia.org/wiki/A*_search_algorithm#Pseudocode).

## Path Smoothing

Since the path is discrete, it can be shortened by connecting two points with a straight line, as long as no collision occurs. A loop checks if each point can be connected to the farthest previous point without causing a collision, using the `isLineColl` function. This ensures the start and end points are included, as they are added before the loop.

<img src="{{ site.baseurl }}/assets/posts/Pathfinding/smooth_unsmooth.png" width="80%"/>

*Figure 4: Left - The Calculated Path, Right - The Smoothed Path  
In Red – the Start and End Points*

## Viola!

Now the robot has a set of points to move toward!
