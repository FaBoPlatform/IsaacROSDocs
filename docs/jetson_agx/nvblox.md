# NVblox


## パッケージの準備

```
cd ${ISAAC_ROS_WS}/src
git clone --recursive -b release-3.2 https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_nvblox.git isaac_ros_nvblox
```

```
cd ${ISAAC_ROS_WS}/src/isaac_ros_nvblox/nvblox_examples/realsense_splitter && \
    git update-index --assume-unchanged COLCON_IGNORE && \
    rm COLCON_IGNORE
```

## Isaac ROS Dockerの起動

!!!Warning
     /dev/fb0 が無いせいで CDI デバイス注入がコケて コンテナ起動に失敗してすので、下記Dockerコンテナ起動前に、必ずディスプレイに接続。

```
cd ${ISAAC_ROS_WS}/src/isaac_ros_common && \
./scripts/run_dev.sh
```

## Realsenseに必要なパッケージのインストール

```
cd /workspaces/isaac_ros-dev
colcon build --symlink-install --packages-up-to realsense_splitter
source install/setup.bash
```

## Isaac ROS パッケージのインストール

```
sudo apt update
sudo apt-get install -y ros-humble-nova-developer-kit-bringup 
source /opt/ros/humble/setup.bash
```

## NVBloxの起動

```
ros2 launch nvblox_examples_bringup realsense_example.launch.py
```

## デモ動画

![YOUTUBE](E8VbMaqGU9Y)

## Referenceページ　

- [Nvblox](https://nvidia-isaac-ros.github.io/concepts/scene_reconstruction/nvblox/index.html)
- [RealSense Camera Examples](https://nvidia-isaac-ros.github.io/concepts/scene_reconstruction/nvblox/tutorials/tutorial_realsense.html)
- [Multi-RealSense Camera Examples](https://nvidia-isaac-ros.github.io/concepts/scene_reconstruction/nvblox/tutorials/tutorial_multi_realsense.html#multi-realsense-camera-examples)
