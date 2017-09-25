This is the project repo for the final project of the Udacity Self-Driving Car Nanodegree: Programming a Real Self-Driving Car. For more information about the project, see the project introduction [here](https://classroom.udacity.com/nanodegrees/nd013/parts/6047fe34-d93c-4f50-8336-b70ef10cb4b2/modules/e1a23b06-329a-4684-a717-ad476f0d8dff/lessons/462c933d-9f24-42d3-8bdc-a08a5fc866e4/concepts/5ab4b122-83e6-436d-850f-9f4d26627fd9).

## Installation

### Docker

Install Docker-CE from [here](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/).
```
 # on Ubuntu 16.04 prefer version 17.06.0~ce-0~ubuntu instead 17.06.0~ce-1~ubuntu
 # because of the issue https://github.com/moby/moby/issues/22207
 # or docker may eat all of your disk space

 sudo apt-get install docker-ce=17.06.0~ce-0~ubuntu

 # add yourself to the docker group and relogin
 sudo usermod -a -G docker username
```

If you have Nvidia GPU install Nvidia-Docker from [here](https://github.com/NVIDIA/nvidia-docker)

```
 # clone this repository
 git clone https://github.com/parilo/CarND-Capstone.git
 cd CarND-Capstone

 # Run and enter the docker container
 # run GPU version of the container
 nvidia-docker run -dit --name udacity-carnd-ros -v "$(pwd)":/home/ros/project --user "$(id -u)" -p 4567:4567 -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix parilo/udacity-carnd-ros-gpu:ver1 bash
 # enter the container
 nvidia-docker exec -it udacity-carnd-ros bash
 
 # run none-GPU version
 docker run -dit --name udacity-carnd-ros -v "$(pwd)":/home/ros/project --user "$(id -u)" -p 4567:4567 -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix parilo/udacity-carnd-ros-nogpu:ver1 bash
 # enter the container
 docker exec -it udacity-carnd-ros bash

 # run this on your host OS in order to be able to run GUI apps
 xhost +

 # you may safely leave the container with exit command and reenter it again

 # compile and run the code
 cd /home/ros/project/ros
 source /opt/ros/kinetic/setup.bash
 catkin_make
 source devel/setup.sh
 roslaunch launch/styx.launch
 # then run simualtor

 # remember that all your modifications of the system in the container
 # will be lost after container removed
 # all changes in /home/ros/project will be preserved

 # stop and remove docker container
 docker container stop udacity-carnd-ros
 docker container rm udacity-carnd-ros

```

[How to build docker images](https://github.com/parilo/CarND-Capstone/blob/master/docker/README.md)

### Native

* Be sure that your workstation is running Ubuntu 16.04 Xenial Xerus or Ubuntu 14.04 Trusty Tahir. [Ubuntu downloads can be found here](https://www.ubuntu.com/download/desktop).
* If using a Virtual Machine to install Ubuntu, use the following configuration as minimum:
  * 2 CPU
  * 2 GB system memory
  * 25 GB of free hard drive space

  The Udacity provided virtual machine has ROS and Dataspeed DBW already installed, so you can skip the next two steps if you are using this.

* Follow these instructions to install ROS
  * [ROS Kinetic](http://wiki.ros.org/kinetic/Installation/Ubuntu) if you have Ubuntu 16.04.
  * [ROS Indigo](http://wiki.ros.org/indigo/Installation/Ubuntu) if you have Ubuntu 14.04.
* [Dataspeed DBW](https://bitbucket.org/DataspeedInc/dbw_mkz_ros)
  * Use this option to install the SDK on a workstation that already has ROS installed: [One Line SDK Install (binary)](https://bitbucket.org/DataspeedInc/dbw_mkz_ros/src/81e63fcc335d7b64139d7482017d6a97b405e250/ROS_SETUP.md?fileviewer=file-view-default)
* Download the [Udacity Simulator](https://github.com/udacity/CarND-Capstone/releases/tag/v1.2).

### Usage

1. Clone the project repository
```bash
git clone https://github.com/udacity/CarND-Capstone.git
```

2. Install python dependencies
```bash
cd CarND-Capstone
pip install -r requirements.txt
```
3. Make and run styx
```bash
cd ros
source /opt/ros/kinetic/setup.bash
catkin_make
source devel/setup.sh
roslaunch launch/styx.launch
```
4. Run the simulator

### Real world testing
1. Download [training bag](https://drive.google.com/file/d/0B2_h37bMVw3iYkdJTlRSUlJIamM/view?usp=sharing) that was recorded on the Udacity self-driving car
2. Unzip the file
```bash
unzip traffic_light_bag_files.zip
```
3. Play the bag file
```bash
rosbag play -l traffic_light_bag_files/loop_with_traffic_light.bag
```
4. Launch your project in site mode
```bash
cd CarND-Capstone/ros
roslaunch launch/site.launch
```
