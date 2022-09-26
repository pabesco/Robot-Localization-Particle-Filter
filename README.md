# Robot-Localization-Particle-Filter
Follows the Coursera MOOC



# Robot Localization using Particle Filter
Let's say a robot has been dropped onto a random location on a distant planet or in an uninhabited area. The robot has no GPS signal available but it has a sensors which measure its elevation.
The robot, however, has the terrain map (geospatial) of the region.
Robot localization is This problem of finding the robots location is called **"Robot Localization"**.
Particle Filter is one of the approach to robot localization.

## Particle Filter
In the particle filter approach, we spawn number of particles (e.g. 3000) on the terrain map randomly. We assign the centre of mass of these particles as the estimated location for our robot.

We then move the robot around on the terrain by moving it forward and providing rotation inputs.

As the robot's position changes, the altitude sensor provides output for the robot's elevation.

We apply the exact motion to the randomly distributed particles as well on the terrain map. 

Each particle is assigned a corresponding weight based on the error in the particle's elevation and the robot's elevation sensor output. 

Since particles with higher errors are less likely to represent the position of the robot and vice versa, the centre of mass of the particles changes as per the weighted average.

Additionally, we also eliminate the particles that move out of the defined region.

As the robot moves, the effect of particles with lower error get amplified and start homing on to the actual location of the robot.

Thus, we can traingulate the robot's location solving the Robot Localization problem.


### Comments on Jupyter Notebook
"map.png" has the terrain map. The grayscale image intensity (pixel reading) gives the indicator of terrain height.

•	Keyboard input of Numpad 8,4 and 6 are taken for forward, right and left turn.

•	A noise is introduced to the robot motion to simulate real world conditions.

•	3000 particles are introduced each with x, y and theta (angle) attributes. A random value between 0 and 1 is generated and multiplied by width, height and 360 degrees, to randomize the location of these particles across the map with different orientations.

•	The error in the actual elevation and particle elevation is normalized (so that lower error has higher value) and cubed to get the corresponding weights of the particles.

•	Particles array is resampled based on the particle weights (probabilities). Thus, particles with higher weights will be resampled more often to form a new Particle array of 3000 particles for each step.

•	The mean (centre of mass) of the particles is calculated to estimate the guess for robot's position.

•	As the robot moves, weight calcuation and resampling occurs thus, improving the best guess for robot's location.

