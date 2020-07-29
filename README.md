***
# Rovio
+ **hardware setup**
    + jetson TX2 - Jetpack 4.2
    + jetson Xavier NX - Jetpack 4.4
    + realsense D435i (color, infra1, infra2)
    + pixhawk4 mini
    <br>
+ **software setup**
    + Ubuntu: 18.04 
    + ROS: Melodic 
    <br>
+ **github link**: [ethz_asl](https://github.com/ethz-asl/rovio)
***
<br>

# Index
### 1. Prerequisites
####    &nbsp;&nbsp;&nbsp;&nbsp;● kindr
####    &nbsp;&nbsp;&nbsp;&nbsp;● lightweight_filtering (as submodule, use "git submodule update --init --recursive")
### 2. Installation
### 3. TX2, NX
####    &nbsp;&nbsp;&nbsp;&nbsp;● Actually, there is no installation difference between TX2 and NX
### 4. Run
<br><br>

## 1. Prerequisites
### ● kindr
+ kindr from [here](https://github.com/ethz-asl/kindr)
```
$ 
```
### ● lightweight_filtering
+ as submodule, use "git submodule update --init --recursive"
```
$ su
```
<br><br>

## 2. Installation
+ git clone and build from source
```
$ cd ~/catkin_ws/src
$ git clone https://github.com/HKUST-Aerial-Robotics/VINS-Mono.git
$ cd ../ && catkin build -DCMAKE_BUILDTYPE=Release -j3
$ source ~/catkin_ws/devel/setup.bash
```
<br><br>

## 3. TX2, NX
#### ● Actually, there is no installation difference between TX2 and NX
<br><br>

## 4. Run
#### ● you have to get a calibration data using [kalibr](https://github.com/zinuok/kalibr)
```
$ roslaunch realsense2_camera rs_camera.launch
$ roslaunch mavros px4.launch
$ roslaunch rovio d435i_rovio_node_mono.launch
```

