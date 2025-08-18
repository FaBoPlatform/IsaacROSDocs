# 環境設定

!!!Info
    Jetson Orin Nova Developer Kitのメモリは64GBなので、Dockerや作業フォルダをSSDに移動します。作業フォルダは必ずSSD側に変更します。

## 作業フォルダをSSDに

Jetson AGX Orinのメモリ 32G or 64Gでは容量がすぐ足りなくなるので、Isaac ROSの作業スペースをSSDに設定。

```
mkdir -p  /mnt/nova_ssd/workspaces/isaac_ros-dev/src
echo "export ISAAC_ROS_WS=/mnt/nova_ssd/workspaces/isaac_ros-dev/" >> ~/.bashrc
source ~/.bashrc
```

## Git LFSのインストール

```
sudo apt-get install git-lfs
git lfs install --skip-repo
```

## Reference

- [Developer Environment Setup](https://nvidia-isaac-ros.github.io/getting_started/dev_env_setup.html)