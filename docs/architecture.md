# Architecture

The ros1-to-ros2-bridge deployment provides interoperability between ROS 1 and ROS 2 ecosystems using the `ros1_bridge` dynamic bridge.

The deployment is containerized and enables bidirectional communication between ROS Noetic and ROS 2 Foxy nodes without requiring modifications to existing applications.

## Component Boundaries

| Component         | Implementation               |
| ----------------- | ---------------------------- |
| ROS 1 Runtime     | ROS Noetic                   |
| ROS 2 Runtime     | ROS 2 Foxy                   |
| Bridge Layer      | `ros1_bridge` dynamic bridge |

## System Architecture

```text
┌─────────────┐
│ ROS 1 Nodes │
└──────┬──────┘
       │
       ▼
┌─────────────────┐
│ Dynamic Bridge  │
│   ros1_bridge   │
└──────┬──────────┘
       │
       ▼
┌─────────────┐
│ ROS 2 Nodes │
└─────────────┘
```

## Runtime Flow

1. A ROS 1 master is started.
2. ROS 1 publishers and subscribers register with the master.
3. ROS 2 DDS discovery becomes available.
4. The dynamic bridge inspects both middleware environments.
5. Matching message definitions are detected automatically.
6. Bidirectional forwarding routes are created.
7. Messages flow transparently between ROS 1 and ROS 2.

## Middleware

The deployment uses CycloneDDS:

```bash
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
```

CycloneDDS provides reliable DDS discovery and communication across distributed deployments.

## Container Contents

The published image contains:

* ROS Noetic
* ROS 2 Foxy
* ros1_bridge
* CycloneDDS
* Runtime startup scripts

## External Dependencies

The deployment requires:

* Docker Engine
* Network connectivity between hosts
* ROS Master availability
* DDS multicast support or equivalent network routing

```
```
