# ZED 2i

## Driverのインストール

[ZED SDK 5.0](https://www.stereolabs.com/en-jp/developers/release/5.0#82af3640d775)をのページから、ZED SDK for JetPack 6.1 and 6.2 (L4T 36.4)をDownloadして、インストール。


## コンテナの起動

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

ZED_Explorerが起動すれば設定成功。

```
/usr/local/zed/tools/ZED_Explorer
```


## Reference

- [https://github.com/jetsonhacks/jetson-orin-librealsense](https://github.com/jetsonhacks/jetson-orin-librealsense)
- [Isaac ROS RealSense Setup](https://nvidia-isaac-ros.github.io/getting_started/hardware_setup/sensors/realsense_setup.html)
- [Firmware releases D400](https://dev.realsenseai.com/docs/firmware-releases-d400)