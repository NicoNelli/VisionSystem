# VisionSystem with Gazebo simulator and PX4 SITL simulation

## Objective:
Landing action using vision system

## Initial setup:

### In the repo folder:

Firstly, load its sub-modules

Then:

	1. Firmware module: branch stable.
	Move to sitl_gazebo folder to load its the submodules, then set the branch VisionSystem.
	It allows to run the PX4 simulator.

	2. mocap2mav module: branch VisionSystem or VisionSystemBeta.
	Load the submodules.
	This module is the guidance controller.

	3. landingPlat module: branch master.
	It's allows to move the platform in Gazebo simulation.

	4. tb3_aprilTag module: branch VisionSystem.
	Then, load sub-module "lcm_bridge".
	It's a ROS workspace in which there are the vision system and the bridge for communicating
	with the guidance controller and a package to set the simulation.

## How to run:

Remember to export the variable M2M_INCLUDE to link the lcm_bridge and the guidance controller.

### To compile Firmware module:
```
cd ~/Firmware
make posix_sitl_default
no_sim=1 make posix_sitl_default gazebo
```

The last instruction will wait to connect to the simulator

### To set the vision system:
```
cd ~/tb3_aprilTag
source environment.sh

### To run the simulation with the vision system:
```
cd ~/tb3_aprilTag/catkin_ws/src/load_simulation
source setup_variable.sh
```
It links Gazebo with Firmware, the bridge with Guidance controller, it includes the plugin for the platform, hence:
```
roslaunch load_simulation load_simulation.launch
```
It runs MAVROS package and aprilTag vision system.


