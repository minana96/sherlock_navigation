# *sherlock_navigation* ROS package

This repository represent the *sherlock_navigation* ROS pacakge, the package that configures and launches navigation task via [ROS navigation stack](http://wiki.ros.org/navigation). Navigation stack consists of muliple ROS packages that can be added as plugins to the [move_base](http://wiki.ros.org/move_base?distro=noetic) ROS node. The *sherlock_navigation* package is intended for ROS Melodic. The repository needs to be cloned to the catkin workspace on the robot (no need to clone it to the PC) and compiled with following commands:
```bash
cd <catkin_ws_dir>/src
git clone git@github.com:minana96/sherlock_navigation.git
cd ..
catkin_make
```

## Dependencies

The package is dependent on variety of ROS pacakges that are part of ROS navigation stack, which can be all installed with the following command:
```bash
sudo apt install ros-melodic-navigation
```

## Package content

The package consists of two directories, namely, *config* and *launch*.

### config

The direcotry contains parameter configurations for *move_base* ROS node and its plugins in *yaml* format, which are passed as arguments when the node is launched:
- **move_base_params.yaml**: the configuration parameters for *move_base* ROS node. The definitions of parameters are available in *move_base* [ROS wiki page](http://wiki.ros.org/move_base?distro=noetic);
- **global_costmap_params.yaml**: the configuration parameters for *global costmap* plugin in *move_base* ROS node. The plugin in use is implemented in *costmap_2d* ROS package, with the the description of all parameters available in its [ROS wiki page](http://wiki.ros.org/costmap_2d?distro=noetic);
- **local_costmap_params.yaml**: the configuration parameters for *local costmap* plugin in *move_base* ROS node. The plugin in use is implemented in *costmap_2d* ROS package, with the the description of all parameters available in its [ROS wiki page](http://wiki.ros.org/costmap_2d?distro=noetic);
- **costmap_common_params.yaml**: the configuration parameters that are common for both *global costmap* and *local costmap* plugins in *move_base* ROS node. Both plugins in use are implemented in *costmap_2d* ROS package, with the the description of all parameters available in its [ROS wiki page](http://wiki.ros.org/costmap_2d?distro=noetic);
- **global_planner_params.yaml**: the configuration parameters for *global planner* plugin in *move_base* ROS node. The plugin in use is implemented in *global_planner* ROS package, with the the description of all parameters available in its [ROS wiki page](http://wiki.ros.org/global_planner?distro=noetic);
- **dwa_local_planner_params.yaml**: the configuration parameters for *local planner* plugin in *move_base* ROS node. The plugin in use is implemented in *dwa_local_planner* ROS package, with the the description of all parameters available in its [ROS wiki page](http://wiki.ros.org/dwa_local_planner?distro=noetic). This is the default configuration for *local planner* that is used in the experiments, with *vx_samples* and *vth_samples* parameters set to 10 and 20, respectively, and *sim_time* parameter set to 1.5;
- **dwa_local_planner_params_samples_20_40.yaml**: the configuration parameters for *local planner* plugin used in the number of velocity samples effect experiment, with *vx_samples* and *vth_samples* parameters set to 20 and 40 for respetive treatments;
- **dwa_local_planner_params_sim_period_3.yaml**: the configuration parameters for *local planner* plugin used in the simulation time effect experiment, with *sim_time* parameter set to 3 for respetive treatments.

### launch

The navigation task is configured and launched via two launch files:
- **sherlock_navigation.launch**: navigation is launched on the local machine, with the possibility of visualisation in [Rviz](http://wiki.ros.org/rviz) tool. If this option is used, both Rviz and *turtlebot3_navigation* ROS package need to be installed with following commands:
```bash
sudo apt install ros-melodic-rviz
sudo apt install ros-melodic-turtlebot3-navigation
```
- **sherlock_navigation_remote.launch**: navigation is launched on the remote machine that is passed as an argument. If this launch file is used, it is important that packages within ROS navigation stack are also installed on the target remote machine.
