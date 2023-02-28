
```
cd ~/catkin_ws
# Activate ROS env
source devel/setup.sh

# Run every time after code change. 
# Compile
catkin_make -j1
# Grant privilege
sudo setcap 'cap_net_raw=pe' devel/lib/radar_driver/radar_publisher

# Launch everything without running roscore seperately. This will hide stdout output, so use ROS_ERROR to print when debugging.
roslaunch radar_driver single_radar.launch iface:=enp0s31f6 port:=31122 capture:=1
```

After launching:
```
# List current topics
rostopic list

# Print raw detections with any of the below
rostopic echo /radar/unfiltered_radar_packet
rostopic echo /radar/unfiltered_radar_packet/Detections
rostopic echo /radar/unfiltered_radar_packet/Detections[0]

# Print filtered detections similarly
rostopic echo /radar/unfiltered_radar_packet
```
