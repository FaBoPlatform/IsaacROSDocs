# ROSBAGへの保存

## Dockerの起動

```
echo $'-v /etc/nova:/etc/nova\n-v /mnt/nova_ssd/recordings:/mnt/nova_ssd/recordings\n-v `realpath ~/.aws`:/home/admin/.aws:ro' > ${ISAAC_ROS_WS}/src/isaac_ros_common/scripts/.isaac_ros_dev-dockerargs
```

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

## パッケージのインストール

```
sudo apt-get install -y ros-humble-isaac-ros-nova-recorder
```

## ROSBAG形式で録画開始(コマンド)

```
ros2 launch isaac_ros_nova_recorder nova_recorder.launch.py config:=nova-developer-kit headless:=True
```

/mnt/nova_ssd/recordings　に保存される


## 設定できる引数

```
ros2 launch isaac_ros_nova_recorder nova_recorder.launch.py --show-args
```

```
Arguments (pass arguments as '<name>:=<value>'):

    'target_container':
        target container
        (default: 'nova_recorder')

    'config':
        sensor configuration file
        (default: '/etc/nova/systeminfo.yaml')

    'topics':
        additional topics to record
        (default: '[]')

    'recording_directory':
        recording directory
        (default: '/mnt/nova_ssd/recordings')

    's3_bucket':
        S3 bucket
        (default: '')

    'enable_wheel_odometry':
        enable segway wheel odometry
        (default: 'True')

    'headless':
        record data without the UI
        (default: 'False')

    'event_recorder':
        enable event recording
        (default: 'False')

    'webserver_port':
        webserver port for the UI
        (default: '8080')

    'retry_count':
        Number of retries if the server fails to start
        (default: '100')

    'retry_delay':
        Delay in seconds between retries
        (default: '2.0')

    'encoder_qp':
        H.264 encoder quality parameter
        (default: '20')
```

## Reference

- [isaac_ros_nova_recorder](https://nvidia-isaac-ros.github.io/repositories_and_packages/isaac_ros_nova/isaac_ros_nova_recorder/index.html#quickstart)

