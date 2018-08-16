**Path Planning** 

**Path planning model**

The goals / steps of this project are the following:
* Implement the path planning
* Keep the car in the simulator on track under the speed limit
* Avoid excessive jerk
* Avoid collisions
* Pass slow cars



---
#### Input and output

The input of the path planner is current position, speed and yaw of the car,
a list of other cars' position and speed, and the previous path.

The output is a series of ponts comprising the planned path.

#### Points generation and fitting spline 

First I define a policy that the car, such as lane and speed to follow based on the given data:

* Check if there is a car too close in front of us (main.cpp:282-297) 
* If there is one choose whether to slow down or change lane (main.cpp:302-331) I used a counter to slow down/speed up softly without exceeding the maximum jerk
* Set desired speed (main.cpp:333-337)

Then based on the choices above (lane and speed) I create some points to fit to the spline:

* Set the first points as the current and previous car position (main.cpp:346-368) 
* Set some points (in this case 3) based on the lane at regular distances (in this case 30 meters), the distance between points also determines how many meters does it take to change lane, because the previous point is the current car position, within the old lane (main.cpp:370-374)
* Convert to relative coordinates, before the spline fitting (main.cpp:376-382)
* Finally the points are fit to the spline(main.cpp:384-385)

#### Path generation

Once we have the spline fit the path generation is quite simple, as the pints are generated at intervals based on the desired velocity:

* First we add the leftover points from previous path (main.cpp:390-393)
* Then we calculate the absolute values for the points of the path (main.cpp:395-418)
* And finally send set them for use (main.cpp:434-435)
