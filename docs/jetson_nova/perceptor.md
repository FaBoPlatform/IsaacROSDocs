# Perceptor

!!!info
    Isaac Pereptorは、Visual SLAM, Visual Global Localization, DNN Stereo Depth, Nvblox, Image Pipelineを用いてカメラベースでロボットの位置推定と3Dマップ作成を同時に行えます。

## 事前準備

## Isaac ROS Dockerの起動

!!!Warning
     /dev/fb0 が無いせいで CDI デバイス注入がコケて コンテナ起動に失敗してすので、下記Dockerコンテナ起動前に、必ずディスプレイに接続。


```
cd ${ISAAC_ROS_WS}/src/isaac_ros_common && \
./scripts/run_dev.sh
```

## Isaac ROS パッケージのインストール


```
sudo apt update
sudo apt-get install -y ros-humble-nova-developer-kit-bringup 
source /opt/ros/humble/setup.bash
```

## 必要なAssetのインストール


```
sudo apt-get install -y ros-humble-isaac-ros-peoplesemseg-models-install ros-humble-isaac-ros-ess-models-install
source /opt/ros/humble/setup.bash
    
ros2 run isaac_ros_ess_models_install install_ess_models.sh --eula
ros2 run isaac_ros_peoplesemseg_models_install install_peoplesemsegnet_vanilla.sh --eula
ros2 run isaac_ros_peoplesemseg_models_install install_peoplesemsegnet_shuffleseg.sh --eula
```


## Defaultの条件で起動

```
ros2 launch nova_developer_kit_bringup perceptor.launch.py
```

## Foxglobeで表示

[nova_developer_kit_bringup/foxglove_layouts](https://github.com/NVIDIA-ISAAC-ROS/nova_developer_kit/tree/main/nova_developer_kit_bringup/foxglove_layouts)から、nova_developer_kit_perceptor.jsonをダウンロードする。


## 設定できるパラメーター

```
ros2 launch nova_developer_kit_bringup perceptor.launch.py --show-args
```

```
Platform detected as: aarch64. Setting negotiation time to: 20
Using container type: component_container_mt, with arguments: ['--ros-args', '--log-level', 'info']
Arguments (pass arguments as '<name>:=<value>'):

    'mode':
        One of: ['real_world', 'simulation', 'rosbag']
        (default: 'real_world')

    'rosbag':
        no description given
        (default: 'None')

    'enabled_fisheye_cameras':
        no description given
        (default: '')

    'enable_cuvslam':
        no description given
        (default: 'True')

    'stereo_camera_configuration':
        One of: ['front_configuration', 'front_people_configuration', 'front_left_right_configuration']
        (default: 'front_left_right_configuration')

    'use_foxglove_whitelist':
        no description given
        (default: 'True')

    'type_negotiation_duration_s':
        no description given
        (default: '20')

    'nvblox_param_filename':
        no description given
        (default: 'params/nvblox_perceptor.yaml')

    'nvblox_after_shutdown_map_save_path':
        no description given
        (default: '')

    'sim_global_frame':
        no description given
        (default: 'odom_vslam')

    'global_frame':
        no description given
        (default: 'map')

    'vslam_odom_frame':
        no description given
        (default: 'odom')

    'vslam_map_frame':
        no description given
        (default: 'map')

    'urdf_override_file':
        no description given
        (default: 'None')

    'namespace':
        ROS namespace
        (default: 'hesai_lidar')

    'replay':
        Enable replay from rosbag
        (default: 'False')

    'ip':
        Hesai source IP address
        (default: '192.168.1.201')

    'run_foxglove':
        no description given
        (default: 'True')

    'run_rviz':
        no description given
        (default: 'False')

    'rviz_config':
        no description given
        (default: 'None')
```

## デモ動画

![YOUTUBE](0q05dlYBYSI)

## Referenceページ　

- [Isaac Perceptor](https://nvidia-isaac-ros.github.io/reference_workflows/isaac_perceptor/index.html)
- [Tutorial: Running Camera-based 3D Perception with Isaac Perceptor with the Nova Orin Developer Kit](https://nvidia-isaac-ros.github.io/reference_workflows/isaac_perceptor/tutorials_on_devkit/demo_perceptor.html)
- [Nova developer kit](https://github.com/NVIDIA-ISAAC-ROS/nova_developer_kit)
- [Nova Orin Developerkit NGC Catalog](https://catalog.ngc.nvidia.com/orgs/nvidia/teams/isaac/containers/nova_developer_kit_bringup/tags)
