# Realsense

## Driverのインストール

[https://github.com/jetsonhacks/jetson-orin-librealsense](https://github.com/jetsonhacks/jetson-orin-librealsense)を参考にしてインストールします。

```
git clone https://github.com/jetsonhacks/jetson-orin-librealsense
```

```
cd jetson-orin-librealsense
```

```
sha256sum -c install-modules.tar.gz.sha256
```

```
tar -xzf install-modules.tar.gz
cd install-modules
```

```
sudo ./install-realsense-modules.sh
```


## librealsenseのインストール

```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE
```

```
sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo $(lsb_release -cs) main" -u
```

```
sudo apt-get install librealsense2-utils
sudo apt-get install librealsense2-dev
```

## 動作確認

```
reboot
```

```
realsense-viewer
```

## 作業フォルダに移動

```
cd ${ISAAC_ROS_WS}/src && \
   git clone -b release-3.2 https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_common.git isaac_ros_common
```

コンテナの設定にrealsenseの設定も追加

```
cd ${ISAAC_ROS_WS}/src/isaac_ros_common/scripts && \
touch .isaac_ros_common-config && \
echo CONFIG_IMAGE_KEY=ros2_humble.realsense > .isaac_ros_common-config
```

## コンテナの起動

!!!Warning
	realsenseパッケージのbuildをおこなうために起動時に時間が相当かかる。そのため、sudo apt install tmuxでtmuxをインストールし、tmuxを起動して下記コマンドを実行するとよい。sshの接続が切れたあとで、再度tmuxのセッションにアクセスする場合は、tmux a -t 0でアクセス可能。

```
cd ${ISAAC_ROS_WS}/src/isaac_ros_common && \
./scripts/run_dev.sh -d ${ISAAC_ROS_WS}
```

Realsense Viewerが起動すれば設定成功。

```
realsense-viewer
```

!!!Warning
	Motion ModuleをOnにするとフリーズ場合、すべてのバージョンを一致させる。Realsense Firmwareは5.13.05のバージョンと完全一致する必要があります。

![](./img/realsense01.jpg)


[RealSense Firmware](https://dev.realsenseai.com/docs/firmware-releases-d400)から、5.13.05をダウンロードして、Versionをあわせてください。違うバージョンではIsaac ROS上で動かなくなります。


## Reference

- [https://github.com/jetsonhacks/jetson-orin-librealsense](https://github.com/jetsonhacks/jetson-orin-librealsense)
- [Isaac ROS RealSense Setup](https://nvidia-isaac-ros.github.io/getting_started/hardware_setup/sensors/realsense_setup.html)
- [Firmware releases D400](https://dev.realsenseai.com/docs/firmware-releases-d400)