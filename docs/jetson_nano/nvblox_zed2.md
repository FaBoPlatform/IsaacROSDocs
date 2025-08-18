# NVblox(zed2i)

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

## ZED SDKのインストール

```
sudo chmod +x ${ISAAC_ROS_WS}/src/isaac_ros_common/docker/scripts/install-zed-aarch64.sh && \
${ISAAC_ROS_WS}/src/isaac_ros_common/docker/scripts/install-zed-aarch64.sh
```

## ZED Wrapperのインストール

```
cd ${ISAAC_ROS_WS} && \
sudo apt update && \
rosdep update && rosdep install --from-paths src/zed-ros2-wrapper --ignore-src -r -y && \
colcon build --symlink-install --packages-up-to zed_wrapper
```

```
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
ros2 launch nvblox_examples_bringup zed_example.launch.py \
camera:=zed2
```

## デモ動画


## Referenceページ　

- [Nvblox](https://nvidia-isaac-ros.github.io/concepts/scene_reconstruction/nvblox/index.html)
- [ZED Camera Examples](https://nvidia-isaac-ros.github.io/concepts/scene_reconstruction/nvblox/tutorials/tutorial_zed.html)
