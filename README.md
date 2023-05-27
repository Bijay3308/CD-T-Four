# CD-T-Four
# Object Detection and Pick-up and Drop-up using TurtleBot 3 Burger- HOME SERVICE ROBOT


## Table of Contents
1. Introduction
2. Installation
3. Usage
4. features

## 1. Introduction
The overall goal of this project is to make a home service rebot which can detect and pick-up and drop-off object inside a house hold using TurtleBot 3 burger. This project deals with Robot Operating System (ROS) & OpenCV (Open-source Computer Vision Library).

OpenCV methods are used for detecting the object and ROS is used for linking perception stage to actuation stage. (The detection script and nodes are implemented in Python)

### 1.1 Sensors & Add-ins Used
1. camera- It can be used for visual recognition and identification of objects, enabling the robot to locate items to pick up or drop off accurately.
2. LiDar-  LIDAR sensors, such as the one commonly used in the TurtleBot 3 Burger, provide a 360-degree view of the robot's surroundings by emitting laser beams and measuring the time it takes for the beams to bounce back. LIDAR is useful for mapping the environment, detecting obstacles, and identifying objects for pick-up and drop-off tasks.
3. Gripper Arm- A gripper or manipulator arm attached to the TurtleBot 3 Burger enables the physical interaction with objects. The gripper can be designed to grasp and release items based on their size, weight, and shape, facilitating the pick-up and drop-off tasks.

## 2. Installation
## PC Setup using:
* Ubuntu 20.04
Download the proper ubuntu 20.04.

[Download Ubuntu](https://releases.ubuntu.com/20.04/)

* ROS noetic
* Install Ubuntu desktop
Follow the instruction below to install Ubuntu on PC

[Install Ubuntu desktop](https://ubuntu.com/tutorials/install-ubuntu-desktop#1-overview)

### 2.1 Install ROS on Remote PC 
Open the terminal with ctrl+Alt+T and the the below commands one ata time.
```
 sudo apt update
 sudo apt upgrade
 wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_noetic.sh
 chmod 755 ./install_ros_noetic.sh 
 bash ./install_ros_noetic.sh
```
![Screenshot 2023-05-26 072948](https://github.com/Bijay3308/CD-T-Four/assets/58104378/31aa09cd-b5bd-44ed-952b-867b9fe32dff)
![Screenshot 2023-05-26 073246](https://github.com/Bijay3308/CD-T-Four/assets/58104378/029b9836-d671-4176-a51a-21776647d402)


###2.1.1 Install Dependent ROS Packages
```
$ sudo apt-get install ros-noetic-joy ros-noetic-teleop-twist-joy \
  ros-noetic-teleop-twist-keyboard ros-noetic-laser-proc \
  ros-noetic-rgbd-launch ros-noetic-rosserial-arduino \
  ros-noetic-rosserial-python ros-noetic-rosserial-client \
  ros-noetic-rosserial-msgs ros-noetic-amcl ros-noetic-map-server \
  ros-noetic-move-base ros-noetic-urdf ros-noetic-xacro \
  ros-noetic-compressed-image-transport ros-noetic-rqt* ros-noetic-rviz \
  ros-noetic-gmapping ros-noetic-navigation ros-noetic-interactive-markers
  ```
  ![Screenshot 2023-05-26 073321](https://github.com/Bijay3308/CD-T-Four/assets/58104378/761d36c9-f8a0-4228-bfd9-cc691bd4977a)

  ###2.1.2 Install TurtleBot3 Packages
  ```
  $ sudo apt install ros-noetic-dynamixel-sdk
  $ sudo apt install ros-noetic-turtlebot3-msgs
  $ sudo apt install ros-noetic-turtlebot3
```
```
$ sudo apt remove ros-noetic-dynamixel-sdk
$ sudo apt remove ros-noetic-turtlebot3-msgs
$ sudo apt remove ros-noetic-turtlebot3
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/src/
$ git clone -b noetic-devel https://github.com/ROBOTIS-GIT/DynamixelSDK.git
$ git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
$ git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
$ cd ~/catkin_ws && catkin_make
$ echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
```
![Screenshot 2023-05-26 044642](https://github.com/Bijay3308/CD-T-Four/assets/58104378/20887920-71ec-47af-8089-9ced8958f9db)

##2.2 SBC Setup using:

* Pen drive
* TurtleBot3 SBC Image (Raspberry Pi 4B (2GB or 4GB) ROS2 Foxy image)
* Raspberry Pi Imager

Following the preparation of a pen drive, downloading the correct image file for my hardware and the ROS version that is foxy, unzipping the downloaded image file, extracting the.img file, saving it to the local disk and burning the image file using a Raspberry Pi Imager was done. Then the following includes:

```Click CHOOSE OS.
Click Use custom and select the extracted .img file from local disk.
Click CHOOSE STORAGE and select the microSD.
Click WRITE to start burning the image.
```

![Veed Recording - 6 November 2022 (1)](https://github.com/Bijay3308/CD-T-Four/assets/58104378/069c348d-e40d-40e8-89f8-deaa2c932839)

GParted GUI utility must be installed first 
``` sudo apt install gparted
```
Next, gparted is launched.

``Select microSD card from the menu (mounted location may vary by system).
Right click on the yellow partition.
Select Resize/Move option.
Drag the right edge of the partition to all the way to the right end.
Click Resize/Move button.
Click the Apply All Operations green check button at the top.
``

### 2.2.2 Configure the WiFi Network Setting
Launch a terminal window, and navigate to the netplan directory on the microSD card and open the 50-cloud-init.yaml file and begin editing it with a superuser permission sudo.
```
cd /media/$USER/writable/etc/netplan
sudo nano 50-cloud-init.yaml
```
Replace the WIFI SSID and WIFI PASSWORD with your wifi SSID and password once the editor has been opened.

Press Ctrl+S to save the document and Ctrl+X to close it.
