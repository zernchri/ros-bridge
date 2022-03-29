# ROS/ROS2 bridge for CARLA simulator

[![Actions Status](https://github.com/carla-simulator/ros-bridge/workflows/CI/badge.svg)](https://github.com/carla-simulator/ros-bridge)
[![Documentation](https://readthedocs.org/projects/carla/badge/?version=latest)](http://carla.readthedocs.io)
[![GitHub](https://img.shields.io/github/license/carla-simulator/ros-bridge)](https://github.com/carla-simulator/ros-bridge/blob/master/LICENSE)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/carla-simulator/ros-bridge)](https://github.com/carla-simulator/ros-bridge/releases/latest)

 This ROS package is a bridge that enables two-way communication between ROS and CARLA. The information from the CARLA server is translated to ROS topics. In the same way, the messages sent between nodes in ROS get translated to commands to be applied in CARLA.

![rviz setup](./docs/images/ad_demo.png "AD Demo")

**This version requires CARLA 0.9.12**

## Features

- Provide Sensor Data (Lidar, Semantic lidar, Cameras (depth, segmentation, rgb, dvs), GNSS, Radar, IMU)
- Provide Object Data (Transforms (via [tf](http://wiki.ros.org/tf)), Traffic light status, Visualization markers, Collision, Lane invasion)
- Control AD Agents (Steer/Throttle/Brake)
- Control CARLA (Play/pause simulation, Set simulation parameters)

## Getting started and documentation

Installation instructions and further documentation of the ROS bridge and additional packages are found [__here__](https://carla.readthedocs.io/projects/ros-bridge/en/latest/).

---


## CARLA SERVER
./CarlaUE4.sh -quality-level=Low -ResX=500 -ResY=500


## CARLA CLIENT 
#### foxy + carla 0.9.12
source /opt/ros/foxy/setup.bash && export CARLA_ROOT=/opt/carla-simulator && export PYTHONPATH=$PYTHONPATH:$CARLA_ROOT/PythonAPI/carla/dist/carla-0.9.12-py3.7-linux-x86_64.egg:$CARLA_ROOT/PythonAPI/carla:/home/sim/venv/carla0912/lib/python3.8/site-packages && cd ~/carla-ros-bridge/ && source install/setup.bash

#### galactic + carla 0.9.12
source /opt/ros/galactic/setup.bash && export CARLA_ROOT=/opt/carla-simulator && export PYTHONPATH=$PYTHONPATH:$CARLA_ROOT/PythonAPI/carla/dist/carla-0.9.12-py3.7-linux-x86_64.egg:$CARLA_ROOT/PythonAPI/carla:/home/sim/venv/carla0912/lib/python3.8/site-packages && cd ~/carla-ros-bridge/ && source install/setup.bash

#### galactic + carla 0.9.13
source /opt/ros/galactic/setup.bash && export CARLA_ROOT=/opt/carla-simulator && export PYTHONPATH=$PYTHONPATH:$CARLA_ROOT/PythonAPI/carla/dist/carla-0.9.13-py3.7-linux-x86_64.egg:$CARLA_ROOT/PythonAPI/carla:/home/sim/venv/carla/lib/python3.8/site-packages && cd ~/carla-ros-bridge/ && source install/setup.bash


### Launch Bridge (always needed). Can be launched on HIL (same machine as carla server) or on local laptop ("client") 
ros2 launch carla_ros_bridge carla_ros_bridge.launch.py timeout:=10.0

### Spawn objects (ego vehicle + sensors are launched). Can be launched on HIL (same machine as carla server) or on local laptop ("client") 
ros2 launch carla_spawn_objects carla_spawn_objects.launch.py spawn_point_ego_vehicle:="spawn_point_ego_vehicle"

### Launch pygame for ego vehicle control. Can only be launched on local laptop because of pygame display restrictions.
add carla venv to PYTHONPATH first and source carla venv:
export PYTHONPATH=$PYTHONPATH:/home/sebastian/Code/venv/carla/lib/python3.8/site-packages && source /home/sebastian/Code/venv/carla/bin/activate
ros2 launch carla_manual_control carla_manual_control.launch.py
