# 地図作成しPerceptor


## 地図作成

```
cd ${ISAAC_ROS_WS}/src/isaac_ros_common && \
  ./scripts/run_dev.sh
```


```
ros2 run isaac_mapping_ros create_map_offline.py \
  --sensor_data_bag=<PATH_TO_BAG> \
  --base_output_folder=<PATH_TO_OUTPUT_FOLDER>
```

## 地図と一緒にPerceptor

```
sudo apt-get install -y ros-humble-isaac-ros-peoplesemseg-models-install \
  ros-humble-isaac-ros-ess-models-install
```

```
source /opt/ros/humble/setup.bash
```

``` 
ros2 run isaac_ros_ess_models_install install_ess_models.sh --eula
ros2 run isaac_ros_peoplesemseg_models_install install_peoplesemsegnet_vanilla.sh --eula
ros2 run isaac_ros_peoplesemseg_models_install install_peoplesemsegnet_shuffleseg.sh --eula
```

地図と一緒にperceptorを起動

```
ros2 launch nova_developer_kit_bringup perceptor.launch.py \
  stereo_camera_configuration:=front_left_right_configuration \
  disable_vgl:=False \
  vslam_load_map_folder_path:=<PATH_TO_MAP_FOLDER>/cuvslam_map/ \
  vgl_map_dir:=<PATH_TO_MAP_FOLDER>/cuvgl_map/ \
  occupancy_map_yaml_file:=<PATH_TO_MAP_FOLDER>/occupancy_map.yaml \
  vslam_enable_slam:=True
```

ROSBAGと一緒にperceptor

```
ros2 launch nova_carter_bringup perceptor.launch.py \
  stereo_camera_configuration:=front_left_right_configuration \
  disable_vgl:=False \
  vslam_load_map_folder_path:=<PATH_TO_MAP_FOLDER>/cuvslam_map/ \
  vgl_map_dir:=<PATH_TO_MAP_FOLDER>/cuvgl_map/ \
  occupancy_map_yaml_file:=<PATH_TO_MAP_FOLDER>/occupancy_map.yaml \
  vslam_enable_slam:=True \
  mode:=rosbag \
  rosbag:=<BAG_PATH>
```

## ROSBAGから地図を作成しperceptor

```
ros2 run isaac_mapping_ros create_map_offline.py \
  --sensor_data_bag=/mnt/nova_ssd/recordings/rosbag2/r2b_galileo_r2b_galileo_0.mcap \
  --base_output_folder=/mnt/nova_ssd/recordings/maps
```

```
ros2 launch nova_carter_bringup perceptor.launch.py \
  osbag:=/mnt/nova_ssd/recordings/rosbag2/r2b_galileo_r2b_galileo_0.mcap \
  mode:=rosbag  \
  stereo_camera_configuration:=front_left_right_configuration \ 
  disable_vgl:=True  \ 
  vslam_load_map_folder_path:=/mnt/nova_ssd/recordings/maps/latest/cuvslam_map \
  occupancy_map_yaml_file:=/mnt/nova_ssd/recordings/maps/latest/occupancy_map.yaml \
  replay_rate:=0.1 \
  vslam_enable_slam:=True
```

## Reference

- [Tutorial: Mapping and Localization with Isaac Perceptor](https://nvidia-isaac-ros.github.io/reference_workflows/isaac_perceptor/tutorial_mapping_and_localization.html)
