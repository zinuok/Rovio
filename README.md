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
####    &nbsp;&nbsp;&nbsp;&nbsp;● lightweight_filtering
### 2. Install
### 3. TX2, NX
####    &nbsp;&nbsp;&nbsp;&nbsp;● Actually, there is no installation difference between TX2 and NX
### 4. Run
<br><br>

## 1. Prerequisites
### ● kindr
+ kindr from [here](https://github.com/ethz-asl/kindr)
```
$ cd ~/catkin_ws/src
$ git clone https://github.com/ANYbotics/kindr
$ cd .. && catkin build -DCMAKE_BUILD_TYPE=Release -j3
```

### ● lightweight_filtering
+ as submodule, use "git submodule update --init --recursive"
```
$ cd ~/catkin_ws/src
$ git clone https://github.com/ethz-asl/rovio
$ cd rovio && git submodule update --init --recursive
```
<br><br>

## 2. Installation

+ **rovio** is set to 'stereo'. However, the 'stereo mode' doesn't work in my case. Fortunately, rovio supports changing **'stereo mode' <-> 'mono mode'**. Let's change the rovio into **'mono'**
<br><br>in ~/rovio/CMakeLists.txt line 5, change
```
set(ROVIO_NCAM 2 CACHE STRING "Number of enabled cameras")
to
set(ROVIO_NCAM 1 CACHE STRING "Number of enabled cameras")
```

+ build from source (already cloned with the lightweight_filtering installation)
```
$ cd ~/catkin_ws/src
$ catkin build rovio -DCMAKE_BUILD_TYPE=Release -j3
$ source ~/catkin_ws/devel/setup.bash
```

+ (optional) install with opengl scene
    + Additional dependencies: opengl, glut, glew
```
$ sudo apt-get install -y freeglut3-dev, sudo apt-get install libglew-dev
$ sudo apt-get install -y freeglut3-dev libglew-dev
$ cd ~/catkin_ws/src
$ catkin build rovio -DCMAKE_BUILD_TYPE=Release -j3 -DMAKE_SCENE=ON
```
<br><br>

## 3. TX2, NX
#### ● Actually, no installation difference between TX2 and NX
<br><br>

## 4. Run
#### ● you have to get a calibration data using [kalibr](https://github.com/zinuok/kalibr)
#### ● I made additional launch file named ['d435i_rovio_node_mono'](https://github.com/zinuok/Rovio/blob/master/d435i_rovio_node_mono.launch) for mono
```
$ roslaunch realsense2_camera rs_camera.launch
$ roslaunch mavros px4.launch
$ roslaunch rovio d435i_rovio_node_mono.launch
```

