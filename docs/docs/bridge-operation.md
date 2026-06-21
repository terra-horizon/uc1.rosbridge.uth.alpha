# Bridge Operation

This document describes the operational procedure for establishing communication between ROS 1 and ROS 2 systems.

## Start the ROS Master

On the ROS 1 host:

```bash
export ROS_IP=<ros1_container_IP>
export ROS_MASTER_URI=http://<ros1_container_IP>:11311

roscore
```

Expected output:

```text
started roslaunch server
ROS_MASTER_URI=http://<ros1_container_IP>:11311
```

## Start the Bridge Container

```bash
docker start -ai <ros_bridge_container_id>
```

Configure the environment:

```bash
source /ros1_bridge_ws/install/setup.bash

export ROS_IP=<ros2_container_IP>
export ROS_MASTER_URI=http://<ros1_container_IP>:11311
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
```

Start the bridge:

```bash
ros2 run ros1_bridge dynamic_bridge --bridge-all-topics
```

Expected output:

```text
created 1to2 bridge for topic '/rosout_agg'
created 2to1 bridge for topic '/rosout'
```

## Verify ROS 2 Discovery

Open a new terminal:

```bash
ros2 topic list
```

Example:

```text
/parameter_events
/rosout
/rosout_agg
```

## Stop the Bridge

Press:

```text
CTRL+C
```

or stop the container:

```bash
docker stop <ros_bridge_container_id>
```
