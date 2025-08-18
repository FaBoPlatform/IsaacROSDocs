# Docker

## Dockerフォルダ

```
/mnt/nova_ssd/docker
```

## Docker daemon.json

```
/etc/docker/daemon.json
```

```
{
    "data-root": "/mnt/nova_ssd/docker",
    "default-runtime": "nvidia",
    "runtimes": {
        "nvidia": {
            "args": [],
            "path": "nvidia-container-runtime"
        }
    }
}
```

## Isaac ROS 3.2で使われるDocker

```
nvcr.io/nvidia/isaac/nova_developer_kit_bringup:release_3.2-aarch64 
```

## Reference

- [Isaac ROS Dev Base](https://catalog.ngc.nvidia.com/orgs/nvidia/teams/isaac/containers/ros/tags)
- [Isaac Perceptor for Nova Orin Developer Kit](https://catalog.ngc.nvidia.com/orgs/nvidia/teams/isaac/containers/nova_developer_kit_bringup)