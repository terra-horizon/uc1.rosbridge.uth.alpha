# TERRA UC1 - Containerized ROS 1 to ROS 2 Bridge Seamless Communication

**Version**: Alpha

This repository provides a complete reference implementation for a **ROS 1 to ROS 2 interoperability bridge**, including Docker-based deployment, networking configuration, and end-to-end validation examples.

It enables seamless communication between:
- ROS 1 Noetic
- ROS 2 Foxy

using a dynamic bridge powered by DDS middleware.

---

## High-Level Architecture & Features

This system implements a containerized robotics communication bridge designed for heterogeneous ROS environments.

### Key Capabilities

- ROS 1 to ROS 2 Dynamic Bridging
- Automatic topic and message type discovery
- Bidirectional communication support
- Containerized deployment using Docker
- DDS-based middleware communication (CycloneDDS)
- Multi-device networking (e.g., Raspberry Pi + bridge host)
- Real-time topic synchronization

---

## Repository Structure

- architecture.md -> System design overview
- bridge-operation.md -> Bridge internals and behavior
- deployment-requirements.md -> Setup requirements
- networking.md -> Networking configuration
- example.md -> End-to-end demo
- troubleshooting.md -> Debugging guide

---

## System Overview

### ROS 1 Layer
- Runs ROS 1 Noetic master (roscore)
- Hosts legacy ROS nodes and publishers

### Bridge Layer
- Runs ros1_bridge dynamic bridge
- Converts ROS 1 to ROS 2 messages automatically

### ROS 2 Layer
- Runs ROS 2 Foxy nodes
- Uses CycloneDDS for discovery and transport

---

## Deployment Example Environment

| Component | Address |
|----------|--------|
| Raspberry Pi 4 (ROS 1 Master) | <ros1_container_IP> |
| Bridge Host | <ros2_container_IP> |
| Middleware | CycloneDDS |
| ROS Versions | Noetic & Foxy |

---

## Run with Docker

Build the image:

docker build -t ros-bridge:amd64 .

Run the service:

docker run -it --net=host --entrypoint /bin/bash ros-bridge:amd64

# Example Deployment Walkthrough

## 1 - Start ROS 1 Master

docker start -ai <ros1_container_id>

export ROS_IP=<ros1_container_IP>

export ROS_MASTER_URI=http://<ros1_container_IP>:11311

roscore

---

## 2 - Start ROS 1 to ROS 2 Bridge

docker start -ai <ros2_container_id>

source /ros1_bridge_ws/install/setup.bash

export ROS_IP=<ros2_container_IP>

export ROS_MASTER_URI=http://<ros1_container_IP>:11311

export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp

ros2 run ros1_bridge dynamic_bridge

---

## 3 - ROS 2 Topic Discovery

ros2 topic list

---

## 4 - ROS 2 Runtime Verification

ros2 node list
ros2 topic info /rosout_agg
ros2 topic echo /rosout_agg

---

## 5 - End-to-End Messaging

rostopic pub /test_topic std_msgs/String "data: 'hello from ros1'"
ros2 topic echo /test_topic

ros2 topic pub /test_topic std_msgs/msg/String "{data: 'hello from ros2'}"
rostopic echo /test_topic

---

## Validation Checklist

- ROS 1 master running
- Bridge container started
- ROS 2 topics visible
- DDS discovery working
- Automatic topic bridging active
- ROS 1 -> ROS 2 works
- ROS 2 -> ROS 1 works

