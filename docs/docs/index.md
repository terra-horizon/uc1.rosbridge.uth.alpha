# TERRA UC1 - Containerized ROS 1 to ROS 2 Bridge

This deployment is Alpha v1.0.0 of the TERRA USV Module ROS Communication Bridge for Use Case 1: assessment of water contamination in coastal areas and in the water cycle. It is a cross-platform, containerized ROS1-to-ROS2 bridge engineered for robust robotic interoperability, ensuring seamless data flow between legacy systems and modern autonomous frameworks.

## Product Chain Components
*   **USV Module ROS Communication Bridge:** Implemented in Alpha v0.0.1. Bridges different versions of the Robot Operating System (ROS) to ensure seamless data flow between legacy systems and modern frameworks.
*   **Autonomous Navigation Workflow Integration:** Foundations only; full end-to-end autonomous navigation integration is planned for a future release.

See [Component 2.XX](https://terra-horizon.github.io/uc1.rosbridge.uth.alpha/) for the scope and status of this component.

## Capabilities
*   **ROS 1 to ROS 2 Dynamic Bridging:** Supports bi-directional, cross-version communication between ROS Noetic and ROS Foxy.
*   **Automatic Topic Discovery:** Dynamically discovers and maps topics and message types across environments at runtime.
*   **Containerized Deployment:** Optimized for rapid deployment and multi-architecture compatibility (x86 and ARM-based edge platforms) using Docker.
*   **DDS Middleware Optimization:** Employs CycloneDDS for optimized discovery, low-latency transport, and real-time topic synchronization.
*   **Multi-Device Networking:** Facilitates seamless multi-device networking (e.g., bridging an edge Raspberry Pi 4 to a master bridge host node).

## Current Scope
This alpha release is a containerized, CLI-driven ROS communication bridge verified during real-world Unmanned Surface Vehicle (USV) field trials at the **Sperchios River**. It does not yet feature automated dynamic custom message type reconfiguration or full integration into the core autonomous navigation loop.

## Main Entry Point

### Build the multi-architecture image

```bash
docker build -t ros-bridge:amd64 .
```

### Spin up the bridge container with host network permissions

```bash
docker run -it --net=host --entrypoint /bin/bash ros-bridge:amd64
```

### Start the dynamic bridge layer

```bash
source /ros1_bridge_ws/install/setup.bash
export ROS_MASTER_URI=http://<ros1_master_IP>:11311
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
ros2 run ros1_bridge dynamic_bridge
```
