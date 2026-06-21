# Troubleshooting

## Bridge Starts But No Topics Appear

Check ROS 2 discovery:

```bash
ros2 topic list
```

Verify ROS Master:

```bash
echo $ROS_MASTER_URI
```

Expected:

```text
http://<ros_bridge_container_IP>:11311
```

---

## No Bridge Routes Created

Check ROS 1 topic types:

```bash
rostopic type /topic_name
```

Check ROS 2 topic types:

```bash
ros2 topic type /topic_name
```

The bridge only creates routes for matching message definitions.

---

## Multiple Network Interfaces

Warning:

```text
using network interface wlan0 selected arbitrarily
```

Specify the desired interface:

```bash
export ROS_IP=<ros2_container_IP>
```

---

## DDS Discovery Problems

Verify middleware:

```bash
echo $RMW_IMPLEMENTATION
```

Expected:

```text
rmw_cyclonedds_cpp
```

---

## Container Diagnostics

Inspect logs:

```bash
docker logs <ros_bridge_container_id>
```

Open a shell:

```bash
docker exec -it <ros_bridge_container_id> bash
```

---

## Verify ROS Master Reachability

```bash
ping <ros_bridge_container_IP>
curl http://<ros_bridge_container_IP>:11311
```
