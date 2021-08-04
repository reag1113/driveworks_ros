# driveworks_ros

## Description

NVIDIA의 SDK for autonomous vehicle software development인 Driveworks의 LaneNet 네트워크를 사용하여 ego-lane을 인식하는 lanenet_ros 패키지, DriveNet 네트워크를 사용하여 물체 인식을 하는 drivenet_ros 패키지로 구성되어 있다.   



### 1. lanenet_ros package
#### Parameters
| Parameter | Type | Description|
| -----|-----|-----|
|image_src| String| Image source topic (Default /image_raw)|
|width|int| Image topic's width|
|height|int| Image topic's height|

#### Subscribed Topic
| Topic | Type | Description|
| -----|-----|-----|
|/image_raw| sensor_msgs::Image|Source image stream to perform detection|

#### Published topic
| Topic | Type | Description|
| -----|-----|-----|
|/lane_pos_xy| autwoare_msgs::LaneArray | Contains the coordinates of left, right lanes in image coordinates|      


### 2. drivenet_ros package
#### Parameters
| Parameter | Type | Description|
| -----|-----|-----|
|image_src| String| Image source topic (Default /image_raw)|
|width|int| Image topic's width|
|height|int| Image topic's height|
|aspectratio|Double| aspect ratio for ROI|

#### Subscribed Topic
| Topic | Type | Description|
| -----|-----|-----|
|/image_raw| sensor_msgs::Image|Source image stream to perform detection|

#### Published topic
| Topic | Type | Description|
| -----|-----|-----|
|/detection/vision_objects | autwoare_msgs::DetectedObjectArray | Contains the coordinates of the bounding box in image coordinates for detected objects|


## Environment

- NVIDIA DRIVE AGX PEGASUS
- Ubutu 18.04
- Docker
- Autoware 
- Driveworks-2.2
- CUDA 10.2


## Getting Started
### Prerequisites

- Driveworks-2.2
- Autoware 

### Installation
```sh
git clone https://github.com/re-ag/driveworks_ros.git 
```

```sh
cp -r driveworks_ros/integrated_viewer ~/Autoware/src/autoware/visualization/
cp -r driveworks_ros/lanenet_ros ~/Autoware/src/autoware/core_perception/
cp -r driveworks_ros/drivenet_ros ~/Autoware/src/autoware/core_perception/
```


```sh
sudo cp driveworks_ros/driveworks.conf /etc/ld.so.conf.d/
sudo ldconfig
```

## Usage


Build **lanenet_ros package, drivenet_ros package**.
```sh
cd ~/Autoware
colcon build --packages-up-to lanenet_ros
colcon build --packages-up-to drivenet_ros
source install/setup.bash
```


### How to launch
```sh
roslaunch lanenet_ros lanenet_ros.launch
roslaunch drivenet_ros drivenet_ros.launch
```


## License



