# Coppelia-ROS2-Integration

## Setting up Coppelia - ROS2

Operating system used here : Ubuntu 20.04.3 LTS

### Adding a data type

Default ros2_interface does not include some data types like 'Twist'. You need to specify it in interfaces.txt and rebuild. 

1) Go to CoppeliaSim default directory and this folder CoppeliaSim/programming/ros2_packages/sim_ros2_interface/meta  
2) Open interfaces.txt and include your required data type. Add `geomtery_msgs/msg/Twist`
3) You may need to install the following plugins for building this package.

```
pip install xmlschema
sudo apt install xsltproc
```

4) In CoppeliaSim/programming/ros2_packages/sim_ros2_interface, open terminal and enter:
    change your coppeliasim folder in first code snippet

```
export COPPELIASIM_ROOT_DIR=~/path/to/coppeliaSim/folder
ulimit -s unlimited #otherwise compilation might freeze/crash
colcon build --symlink-install --cmake-args -DCMAKE_BUILD_TYPE=Release -DLIBPLUGIN_DIR=$COPPELIASIM_ROOT_DIR/programming/libPlugin
```

### Lua script in CoppeliaSim

1) Open coppeliasim by `./coppeliaSim.sh` in default directory of CoppeliaSim, or by shortcuts.
2) Drag and Drop the .ttt file in this repo, or by 'Open Scene'
3) Lua script is attached to the bot. Understand the code, this bot subscribes to topic created by keyboard node. (many functions of simROS (ROS1) are deprecated)
4) If you have ROS2 installed, ROS2 plugin have already loaded when coppelia is launched (you can see it in terminal)
5) "/sim_ros2_interface" node is automatically created. Check by `ros2 node list`

### Install Teleop_twist_keyboard

replace with your ros-version
eg: sudo apt-get install ros-foxy-teleop-twist-keyboard
 
```
sudo apt-get install ros-<ros-version>-teleop-twist-keyboard
```

### Launch ROS2 and start simulation

1) Open different terminal
2) Run keyboard node

```
ros2 run teleop_twist_keyboard  teleop_twist_keyboard 
```
3) This keyboard node publishes to "/cmd_vel". Check by `ros2 topic list`
4) Start simulation in CoppeliaSim.
5) Control the bot with following buttons

> u i o
> 
> j k l
> 
> m , .

#### Refer the video below about 'CoppeliaSim - ROS1' integration. It may help. Be aware of deprecated functons and other changes. 

https://www.youtube.com/watch?v=v3IyN6lRG5A&t=1150s
