# Deployment Requirements

## Supported Platforms

| Platform                | Status    |
| ----------------------- | --------- |
| Ubuntu 20.04            | Supported |
| Docker Engine 24+       | Supported |
| Raspberry Pi 4 & 5 (64-bit) | Supported |
| x86_64 Linux            | Supported |

## Minimum Requirements

| Resource | Requirement                     |
| -------- | ------------------------------- |
| CPU      | 2 cores                         |
| RAM      | 4 GB                            |
| Disk     | 5 GB                            |
| Network  | Layer 2 or Layer 3 connectivity |

## Docker Installation Verification

```bash
docker --version
docker compose version
```

## Pulling the Image

```bash
docker push losandriana/ros1-to-ros2-bridge:tagname
```

## Network Requirements

The following services must be reachable:

| Service         | Port        |
| --------------- | ----------- |
| ROS Master      | 11311/TCP   |
| DDS Discovery   | Dynamic UDP |
| Docker Networks | Internal    |

## Verification

Verify connectivity to the ROS master:

```bash
ping <ros1_container_IP>
curl http://<ros1_container_IP>:11311
```
