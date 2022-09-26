# Robot-Localization-Particle-Filter
Follows the [Coursera Guided Project](https://www.coursera.org/projects/robot-localization-python-particle-filter) 



# Robot Localization using Particle Filter
Imagine a rover on an unknown location on a distant planet or remote area. The rover has no GPS signal and needs to find it's way around.

The rover has two things:
> The terrain map (geospatial) of the region.
> Elevation sensors

The challenge of determining the rover's location on the map is called **"Robot Localization"** problem.

Particle Filter is one of the approaches to solving robot localization.

## Particle Filter
In the particle filter approach, we spawn a large number of particles (e.g. 3000) on the terrain map randomly. 

We assign the centre of mass of these particles as the estimated location for our rover.

We then move the rover around on the terrain by moving providing logitudinal and rotational inputs.

As the eover's position changes, the altitude sensor provides output for the rover's elevation.

We apply the exact motion to the randomly distributed particles on the terrain map as well. 

Each particle is assigned a corresponding weight based on the error between the particle's elevation and the rover's elevation (sensor output). 

Since particles with higher errors are less likely to represent the position of the rover. The weight associated with each particle varies inversely with the error. Thus, lower error particles contributed higher to the centre of mass determination.

Additionally, we also eliminate the particles that move out of the specified region (map).

As the robot moves, the effect of particles with lower error get amplified and the centre of mass starts homing on to the actual location of the rover.

Thus, we can traingulate the rover's location solving the Robot Localization problem.


### Comments on Jupyter Notebook
"map.png" has the terrain map. The grayscale image intensity (pixel reading) gives the indicator of terrain height.

•	Keyboard input of Numpad 8,4 and 6 are taken for forward, right and left turn.

•	A noise is introduced to the robot motion to simulate real world conditions.

•	3000 particles are introduced each with x, y and theta (angle) attributes. A random value between 0 and 1 is generated and multiplied by width, height and 360 degrees, to randomize the location of these particles across the map with different orientations.

•	The error in the actual elevation and particle elevation is normalized (so that lower error has higher value) and cubed to get the corresponding weights of the particles.

•	Particles array is resampled based on the particle weights (probabilities). Thus, particles with higher weights will be resampled more often to form a new Particle array of 3000 particles for each step.

•	The mean (centre of mass) of the particles is calculated to estimate the guess for robot's position.

•	As the robot moves, weight calcuation and resampling occurs thus, improving the best guess for robot's location.

