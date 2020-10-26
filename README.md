# Turtlebot3 LiDAR
***
**Describe: This is a tutorial of using gazebo to simulate navigation algorithm using LiDAR with SLAM algorithm on turtlebot3, which needs a powerful computing power. **

***
##### Develop Environment

+ CPU: AMD Ryzen7 4800U  8C16T
+ GPU: AMD Radeon Graphics × 16 
+ Memory: 8GB * 2 DDR4 3200
+ Disk: SK Hynix 512GB SSD
+ Operating System: Ubuntu18.04.1
+ Linux Kernel:  5.4.0-52-generic

***



##### Install Gazebo Components

```bash
$sudo apt install ros-melodic-gazebo-ros-pkgs ros-melodic-gazebo-msgs ros-melodic-gazebo-plugins ros-melodic-gazebo-ros-control
$cd ~/.gazebo/ && mkdir -p models && cd models/
$wget http://file.ncnynl.com/ros/gazebo_models.txt
$wget -i gazebo_models.txt
$ls model.tar.g* | xargs -n1 tar xzvf
$ls model.tar.g* | xargs -n1 rm
```

##### Test Gazebo

```bash
$screen -dmS roscore roscore
$rosrun gazebo_ros gazebo
```

If all button can be push and modules can be found, go on.

***

##### Install Turtlebot Package And SLAM Package

```bash
$sudo apt-get install ros-melodic-turtlebot3 ros-melodic-turtlebot3-description ros-melodic-turtlebot3-gazebo ros-melodic-turtlebot3-msgs ros-melodic-turtlebot3-slam ros-melodic-turtlebot3-teleop
$sudo apt-get install ros-melodic-slam-karto
$sudo apt-get install ros-melodic-navigation
```

##### Set The Model

```bash
$echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc
$source ~/.bashrc
```

##### Make Project And Create Map

```bash
$cd Turtlebot3_LIDAR/ && catkin_make -j 8
$echo "source /home/username/Turtlebot3_LIDAR/devel/setup.sh" >> ~/.bashrc
#change "/home/username/Turtlebot3_LIDAR" to your directory
$source ~/.bashrc
$roslaunch turtlebot3_gazebo turtlebot3_house.launch
$sudo chmod +x src/turtlebot3/turtlebot3_teleop/nodes/turtlebot3_teleop_key
$roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
#control turtlebot3 using this console
$roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=karto
```

##### Save Map And Navigation

```bash
$mkdir -p ~/maps
$rosrun map_server map_saver -f ~/maps/housemap
#shutdown other console
$roslaunch turtlebot3_gazebo turtlebot3_house.launch
$roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=/home/username/maps/housemap.yaml
#change "/home/username/" to your home directory
```

