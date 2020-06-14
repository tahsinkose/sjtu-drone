# About sjtu_drone #

sjtu_drone is a quadrotor simulation program forked from ['tum_simulator'] (http://wiki.ros.org/tum_simulator) , which is developed with ROS + Gazebo. It is used for testing visual SLAM algorithms aiding with different sensors, such as IMU, sonar range finder and laser range finder. Here by 'sjtu', it means Shanghai Jiao Tong University. Currently, this program is used for testing algorithms for [UAV contest in SJTU](http://mediasoc.sjtu.edu.cn/wordpress)

# Requirements #
This package is compatible with ROS Melodic version (Ubuntu 18.04). Existing versions on the internet support at most until Gazebo 7. After Gazebo 8.0, the API has gone significant changes; therefore, it was necessary to adapt the package to Gazebo 8.0+ API. As the default version of Gazebo coming with ROS Melodic is 7.0, it is suggested that do not use the full installation but the desktop installation.
```
$ sudo apt-get install ros-melodic-desktop
```
# Download and Compiling #
```
$ cd <catkin_ws>/src
$ git clone https://github.com/tahsinkose/sjtu-drone.git
$ cd <catkin_ws>
$ catkin build
```

Here <catkin_ws> is the path of the catkin workspace. Please refer to the [tutorial](http://wiki.ros.org/ROS/Tutorials) about how to create a catkin workspace in ROS.

# Run
The simplest way is calling after you have built the workspace successfully.

```
$ cd <where you check out the code>
$ source devel/setup.bash
$ roslaunch sjtu_drone simple.launch
```
# Running with keyboard
In second terminal:

```
$ rosrun sjtu_drone drone_keyboard
```
# Adding drone to the simulation world
In ROS codespace, the robots are generally added to the environment by `spawn_model` node of `gazebo_ros` package via feeding the corresponding URDF file. However, in this case there isn't any URDF file. In future I might add a simple URDf file just trivially produces a base link for the entire robot. However, current method is directly adding to the all `.world` files as follows:

```
<include>
    <uri>model://sjtu_drone</uri>
    <pose>0 0 1 0 0 0</pose>
</include>
```


# Read sensor data from ROS topics #
One can use [rqt_gui](http://wiki.ros.org/rqt_gui) to have an extensive amount of utilities for topic visualization and manipulation. Some of the useful topics reside below.
```
forward looking camera :  /drone/front_camera/image_raw
downward looking camera: /drone/down_camera/image_raw
sonar data:  /drone/sonar
laser range data: /drone/laser
```