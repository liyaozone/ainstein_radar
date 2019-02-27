# radar_ros_interface:
ROS nodes for interfacing with various radars based on a generic interface message format common to all radars.

Currently supported radars include:

- K79
- T79 with BSD firmware

## Package Dependencies

[radar_sensor_msgs](https://github.com/AinsteinAI/radar_sensor_msgs) : Package defining custom radar message types. 

## Package Structure

```
radar_ros_interface/
├── CMakeLists.txt
├── include
│   └── radar_ros_interface
│       ├── config_t79_bsd.h
│       ├── radardata_to_laserscan.h
│       ├── radardata_to_pointcloud.h
│       ├── radar_interface.h
│       ├── radar_interface_k79.h
│       └── radar_interface_t79_bsd.h
├── launch
│   └── k79_node.launch
├── LICENSE
├── package.xml
├── readme.md
├── scripts
│   └── k79_gui.py
└── src
    ├── k79_node.cpp
    ├── radardata_to_laserscan.cpp
    ├── radardata_to_laserscan_node.cpp
    ├── radardata_to_pointcloud.cpp
    ├── radardata_to_pointcloud_node.cpp
    ├── radar_interface_k79.cpp
    ├── radar_interface_t79_bsd.cpp
    └── t79_bsd_node.cpp
```				

## Supported Radars and Usage

### K79:

The file k79_node.cpp implements a ROS node using the RadarNodeK79 interface class to create a UDP socket bound to the host IP address and port (which must match the radar's configuration), launch a thread to read and publish data to the RadarData message type.

*Command line usage:*	

```bash
rosrun radar_ros_interface k79_node --host-ip HOST_IP_ADDRESS --radar-ip RADAR_IP_ADDRESS [--radar-port RADAR_UDP_PORT] [--host-port HOST_UDP_PORT] [--name RADAR_NAME] [--frame RADAR_FRAME_ID]
```

If unspecified, radar port defaults to 8, host port defaults to 1024, name defaults to "k79" and frame id defaults to "map".

*Example launch file usage (from launch/k79_node.launch):*

```xml
<launch>
  <node name="k79_node" pkg="radar_ros_interface" type="k79_node" args="--host-ip 10.0.0.75 --host-port 1024 --radar-ip 10.0.0.11 --radar-port 7" output="screen" required="true" />
</launch>
```

### T79:

TODO