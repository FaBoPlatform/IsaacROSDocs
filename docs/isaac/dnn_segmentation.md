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

PeopleSemSegnet Model

```
sudo apt-get install -y ros-humble-isaac-ros-peoplesemseg-models-install &&
ros2 run isaac_ros_peoplesemseg_models_install install_peoplesemsegnet_vanilla.sh --eula &&
ros2 run isaac_ros_peoplesemseg_models_install install_peoplesemsegnet_shuffleseg.sh --eula
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
ros2 launch isaac_ros_unet isaac_ros_unet_tensor_rt_isaac_sim.launch.py engine_file_path:=${ISAAC_ROS_WS}/isaac_ros_assets/models/peoplesemsegnet/deployable_quantized_vanilla_unet_onnx_v2.0/1/model.plan input_binding_names:=['input_1:0']
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
ros2 run rqt_image_view rqt_image_view
```


## ROS topic list

```
ros2 topic list
```

```
/back_stereo_imu/imu
/chassis/imu
/chassis/odom
/clock
/cmd_vel
/dnn_image_encoder/converted/image
/dnn_image_encoder/converted/image/nitros
/dnn_image_encoder/crop/camera_info
/dnn_image_encoder/crop/camera_info/nitros
/dnn_image_encoder/crop/image
/dnn_image_encoder/crop/image/nitros
/dnn_image_encoder/crop/image/nitros/nitros_image_rgb8
/dnn_image_encoder/image_tensor
/dnn_image_encoder/image_tensor/nitros
/dnn_image_encoder/normalized_tensor
/dnn_image_encoder/normalized_tensor/nitros
/dnn_image_encoder/resize/camera_info
/dnn_image_encoder/resize/camera_info/nitros
/dnn_image_encoder/resize/image
/dnn_image_encoder/resize/image/nitros
/front_3d_lidar/lidar_points
/front_stereo_camera/left/camera_info
/front_stereo_camera/left/camera_info/nitros
/front_stereo_camera/left/image_rect_color
/front_stereo_camera/left/image_rect_color/nitros
/front_stereo_camera/right/camera_info
/front_stereo_camera/right/image_rect_color
/front_stereo_imu/imu
/left_stereo_imu/imu
/parameter_events
/right_stereo_imu/imu
/rosout
/tensor_pub
/tensor_pub/nitros
/tensor_pub/nitros/nitros_tensor_list_nchw_bgr_f32
/tensor_sub
/tensor_sub/nitros
/tf
/unet/colored_segmentation_mask
/unet/colored_segmentation_mask/nitros
/unet/raw_segmentation_mask
/unet/raw_segmentation_mask/nitros
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
ros2 launch isaac_ros_examples isaac_ros_examples.launch.py launch_fragments:=argus_mono,rectify_mono,unet engine_file_path:=${ISAAC_ROS_WS}/isaac_ros_assets/models/peoplesemsegnet/deployable_quantized_vanilla_unet_onnx_v2.0/1/model.plan input_binding_names:=['input_1:0'] output_binding_names:=['argmax_1'] network_output_type:='argmax'
```

## Reference

- [Tutorial for DNN Image Segmentation with Isaac Sim](https://nvidia-isaac-ros.github.io/concepts/segmentation/unet/tutorial_isaac_sim.html)
- [isaac_ros_unet](https://nvidia-isaac-ros.github.io/repositories_and_packages/isaac_ros_image_segmentation/isaac_ros_unet/index.html#quickstart)
- [Isaac Sim Tutorials](https://nvidia-isaac-ros.github.io/getting_started/index.html#isaac-sim-tutorials)
