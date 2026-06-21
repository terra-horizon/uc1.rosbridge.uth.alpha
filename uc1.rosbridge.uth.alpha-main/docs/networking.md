# Networking

The bridge requires direct network connectivity between ROS 1 and ROS 2 environments.

## Example Topology

```text
┌──────────────┐
│ ROS Master   │
│192.168.XX.XXX│
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ ROS Bridge   │
│192.168.XX.YYY│
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ ROS 2 Nodes  │
└──────────────┘
```

## ROS 1 Configuration

```bash
export ROS_IP=192.168.XX.XXX
export ROS_MASTER_URI=http://192.168.XX.XXX:11311
```

## ROS 2 Configuration

```bash
export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
```

## Connectivity Tests

Verify network reachability:

```bash
ping 192.168.XX.XXX
```

Verify ROS Master accessibility:

```bash
curl http://192.168.XX.XXX:11311
```

Verify topic visibility:

```bash
rostopic list
```

## Common Networking Issues

* Incorrect ROS_IP values
* Multiple active interfaces
* Firewall restrictions
* Docker bridge isolation
* DDS discovery blocked by network policies

```
```
