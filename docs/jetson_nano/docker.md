# Docker


## Dockerの修正

```
sudo usermod -aG docker $USER
id nvidia | grep docker
newgrp docker
```

Dockerを停止

```
sudo systemctl stop docker
```

Docker関連フォルダの移動

```
sudo du -csh /var/lib/docker/ && \
    sudo mkdir /mnt/nova_ssd/docker && \
    sudo rsync -axPS /var/lib/docker/ /mnt/nova_ssd/docker/ && \
    sudo du -csh  /mnt/nova_ssd/docker/
```

`/etc/docker/daemon.json`を修正


```
{
    "runtimes": {
        "nvidia": {
            "path": "nvidia-container-runtime",
            "runtimeArgs": []
        }
    },
    "default-runtime": "nvidia",
    "data-root": "/mnt/nova_ssd/docker"
}
```

古いDockerフォルダをrename

```
sudo mv /var/lib/docker /var/lib/docker.old
```

Dockerの再起動テスト

```
sudo systemctl daemon-reload && \
    sudo systemctl restart docker && \
    sudo journalctl -u docker
```
