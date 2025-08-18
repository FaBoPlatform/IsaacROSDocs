# 環境設定

## 作業フォルダの設定

`SSD`

```
mkdir -p  /mnt/nova_ssd/workspaces/isaac_ros-dev/src
echo "export ISAAC_ROS_WS=/mnt/nova_ssd/workspaces/isaac_ros-dev/" >> ~/.bashrc
source ~/.bashrc
```

`SDカード`を使う場合


```
mkdir -p  ~/workspaces/isaac_ros-dev/src
echo "export ISAAC_ROS_WS=~/workspaces/isaac_ros-dev/" >> ~/.bashrc
source ~/.bashrc
```

## Git LFSのインストール

```
sudo apt-get install git-lfs
git lfs install --skip-repo
```

## Reference

- [Developer Environment Setup](https://nvidia-isaac-ros.github.io/getting_started/dev_env_setup.html)