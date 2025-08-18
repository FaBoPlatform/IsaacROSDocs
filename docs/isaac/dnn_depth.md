# DNN Image Segmentation

## Isaac SIMの起動

```
export ROS_DOMAIN_ID=1
```

Isaac SIMを起動。起動時にROS Bridgeを設定する。


![](./img/isaac_apritag00.jpg)

![](./img/isaac_apritag01.jpg)

![](./img/isaac_apritag02.jpg)


## Jetson側のROSの設定

```
cd ${ISAAC_ROS_WS}/src/isaac_ros_common && \
./scripts/run_dev.sh
```

```
sudo apt update
sudo apt-get install -y ros-humble-nova-developer-kit-bringup 
source /opt/ros/humble/setup.bash
```

```
sudo apt-get install -y ros-humble-isaac-ros-detectnet \
	ros-humble-isaac-ros-dnn-image-encoder \
	ros-humble-isaac-ros-triton
sudo apt-get install -y ros-humble-isaac-ros-examples ros-humble-isaac-ros-argus-camera
```

## Jetson側のコマンド(Terminal1)

Isaac SIMの起動しているPCのROS_DOMAIN_IDと同じIDを指定します。

```
export ROS_DOMAIN_ID=1
```

```
ros2 launch isaac_ros_ess isaac_ros_ess_isaac_sim.launch.py \
   engine_file_path:=${ISAAC_ROS_WS:?}/isaac_ros_assets/models/dnn_stereo_disparity/dnn_stereo_disparity_v4.1.0_onnx/ess.engine \
   threshold:=0.4
```

## Jetson側のコマンド(Terminal2)

Isaac SIMの起動しているPCのROS_DOMAIN_IDと同じIDを指定します。

```
export ROS_DOMAIN_ID=1
```

```
cd ${ISAAC_ROS_WS}/src/isaac_ros_common && \
./scripts/run_dev.sh
```

```
ros2 run isaac_ros_ess isaac_ros_ess_visualizer.py
```


## ROS topic list

```
ros2 topic list
```

```
/back_stereo_imu/imu
/camera_info
/camera_info/nitros
/chassis/imu
/chassis/odom
/clock
/cmd_vel
/disparity
/disparity/nitros
/front_3d_lidar/lidar_points
/front_stereo_camera/left/camera_info
/front_stereo_camera/left/camera_info/nitros
/front_stereo_camera/left/camera_info_resize
/front_stereo_camera/left/camera_info_resize/nitros
/front_stereo_camera/left/image_rect_color
/front_stereo_camera/left/image_rect_color/nitros
/front_stereo_camera/left/image_resize
/front_stereo_camera/left/image_resize/nitros
/front_stereo_camera/right/camera_info
/front_stereo_camera/right/camera_info/nitros
/front_stereo_camera/right/camera_info_resize
/front_stereo_camera/right/camera_info_resize/nitros
/front_stereo_camera/right/image_rect_color
/front_stereo_camera/right/image_rect_color/nitros
/front_stereo_camera/right/image_resize
/front_stereo_camera/right/image_resize/nitros
/front_stereo_imu/imu
/left_stereo_imu/imu
/parameter_events
/points2
/points2/nitros
/right_stereo_imu/imu
/rosout
/tf
```

## Orin Nova Developer Kitのカメラの場合

```
cd ${ISAAC_ROS_WS}/src/isaac_ros_common && \
./scripts/run_dev.sh
```

```
sudo apt-get update
sudo apt-get install -y ros-humble-isaac-ros-examples \
	ros-humble-isaac-ros-argus-camera
```

```
sudo apt-get install -y ros-humble-isaac-ros-examples ros-humble-isaac-ros-argus-camera
```

```
ros2 launch isaac_ros_examples isaac_ros_examples.launch.py \
	launch_fragments:=argus_stereo,rectify_stereo,ess_disparity \
	engine_file_path:=${ISAAC_ROS_WS}/isaac_ros_assets/models/dnn_stereo_disparity/dnn_stereo_disparity_v4.1.0_onnx/ess.engine \
	threshold:=0.4
```

## Reference

- [Tutorial for ESS with Isaac Sim](https://nvidia-isaac-ros.github.io/concepts/stereo_depth/ess/tutorial_isaac_sim.html)
- [isaac_ros_ess](https://nvidia-isaac-ros.github.io/repositories_and_packages/isaac_ros_dnn_stereo_depth/isaac_ros_ess/index.html#quickstart)
- [Isaac Sim Tutorials](https://nvidia-isaac-ros.github.io/getting_started/index.html#isaac-sim-tutorials)
