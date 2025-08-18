# SSD

!!!Info
    Jetson Orin Nova Developer Kitのメモリは64GBなので、Dockerや作業フォルダをSSDに移動します。Dockerイメージが大きいために、標準のメモリ64GBではすぐにディスク容量がいっぱいになってしまい期待した動作ができなくなります。


## SSDデバイスの確認

```
lspci
```

```
0001:00:00.0 PCI bridge: NVIDIA Corporation Device 229e (rev a1)
0001:01:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8822CE 802.11ac PCIe Wireless Network Adapter
0004:00:00.0 PCI bridge: NVIDIA Corporation Device 229c (rev a1)
0004:01:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller PM9A1/PM9A3/980PRO
```

`0004:01:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller PM9A1/PM9A3/980PRO`がSSD


## マウント先の確認

```
lsblk
```

```
NAME         MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0          7:0    0     4K  1 loop /snap/bare/5
loop1          7:1    0  68.8M  1 loop /snap/core22/1752
loop2          7:2    0  68.9M  1 loop /snap/core22/2049
loop3          7:3    0 235.1M  1 loop /snap/firefox/5888
loop4          7:4    0 230.5M  1 loop /snap/firefox/6563
loop5          7:5    0 483.3M  1 loop /snap/gnome-42-2204/178
loop6          7:6    0 493.5M  1 loop /snap/gnome-42-2204/201
loop7          7:7    0  91.7M  1 loop /snap/gtk-common-themes/1535
loop8          7:8    0  38.7M  1 loop /snap/snapd/23772
loop9          7:9    0  42.9M  1 loop /snap/snapd/24787
loop10         7:10   0    16M  1 loop 
mmcblk0      179:0    0  59.3G  0 disk 
├─mmcblk0p1  179:1    0  57.8G  0 part /
├─mmcblk0p2  179:2    0   128M  0 part 
├─mmcblk0p3  179:3    0   768K  0 part 
├─mmcblk0p4  179:4    0  31.6M  0 part 
├─mmcblk0p5  179:5    0   128M  0 part 
├─mmcblk0p6  179:6    0   768K  0 part 
├─mmcblk0p7  179:7    0  31.6M  0 part 
├─mmcblk0p8  179:8    0    80M  0 part 
├─mmcblk0p9  179:9    0   512K  0 part 
├─mmcblk0p10 179:10   0    64M  0 part /boot/efi
├─mmcblk0p11 179:11   0    80M  0 part 
├─mmcblk0p12 179:12   0   512K  0 part 
├─mmcblk0p13 179:13   0    64M  0 part 
├─mmcblk0p14 179:14   0   400M  0 part 
└─mmcblk0p15 179:15   0 479.5M  0 part 
mmcblk0boot0 179:32   0  31.5M  1 disk 
mmcblk0boot1 179:64   0  31.5M  1 disk 
zram0        252:0    0   2.6G  0 disk [SWAP]
zram1        252:1    0   2.6G  0 disk [SWAP]
zram2        252:2    0   2.6G  0 disk [SWAP]
zram3        252:3    0   2.6G  0 disk [SWAP]
zram4        252:4    0   2.6G  0 disk [SWAP]
zram5        252:5    0   2.6G  0 disk [SWAP]
zram6        252:6    0   2.6G  0 disk [SWAP]
zram7        252:7    0   2.6G  0 disk [SWAP]
zram8        252:8    0   2.6G  0 disk [SWAP]
zram9        252:9    0   2.6G  0 disk [SWAP]
zram10       252:10   0   2.6G  0 disk [SWAP]
zram11       252:11   0   2.6G  0 disk [SWAP]
nvme0n1      259:0    0   1.8T  0 disk 
```

## SSDにマウント

```
sudo mkfs.ext4 /dev/nvme0n1
sudo mkdir -p /mnt/nova_ssd
sudo mount /dev/nvme0n1 /mnt/nova_ssd
```

```
lsblk -f
```

```
NAME FSTYPE FSVER LABEL UUID                                 FSAVAIL FSUSE% MOUNTPOINTS
nvme0n1                                                                               
└─nvme0n1p1  ext4     1.0         2c3bd0ed-bdb7-4ab4-8325-2d75b49da9de    1.6T     4% /mnt/nova_ssd
```

UUIDをコピー。

/etc/fstabにマウントフォルダをUUIDベースで追加

```
# /etc/fstab: static file system information.
#
# These are the filesystems that are always mounted on boot, you can
# override any of these by copying the appropriate line from this file into
# /etc/fstab and tweaking it as you see fit.  See fstab(5).
#
# <file system> <mount point>             <type>          <options>                               <dump> <pass>
/dev/root            /                     ext4           defaults                                     0 1
UUID=7802-A31C /boot/efi vfat defaults 0 1
UUID=2c3bd0ed-bdb7-4ab4-8325-2d75b49da9de /mnt/nova_ssd/ ext4 defaults 0 2
```

## オーナーを変更

```
sudo chown ${USER}:${USER} /mnt/nova_ssd
```

## 最終確認

```
sudo blkid | grep nvme
```

```
/dev/nvme0n1p1: UUID="2c3bd0ed-bdb7-4ab4-8325-2d75b49da9de" BLOCK_SIZE="4096" TYPE="ext4" PARTLABEL="primary" PARTUUID="73f67677-5af3-4d06-8821-867d97527640"
```

```
df -h
```

```
Filesystem       Size  Used Avail Use% Mounted on
/dev/mmcblk0p1    54G   38G   14G  74% /
tmpfs             31G  172K   31G   1% /dev/shm
tmpfs             13G   27M   13G   1% /run
tmpfs            5.0M  4.0K  5.0M   1% /run/lock
/dev/mmcblk0p10   63M  118K   63M   1% /boot/efi
/dev/nvme0n1p1   1.8T   68G  1.7T   4% /mnt/nova_ssd
tmpfs            6.2G  120K  6.2G   1% /run/user/1000
```

```
sudo ls -l /mnt/nova_ssd/docker/
```

```
total 96
drwx--x--x   4 root root  4096 Nov 23  2024 buildkit
drwx--x---  27 root root  4096 Aug 11 18:13 containers
-rw-------   1 root root    36 Nov 23  2024 engine-id
drwx------   3 root root  4096 Nov 23  2024 image
drwxr-x---   3 root root  4096 Nov 23  2024 network
drwx--x--- 236 root root 53248 Jan  1  1970 overlay2
drwx------   4 root root  4096 Nov 23  2024 plugins
drwx------   2 root root  4096 Jan  1  1970 runtimes
drwx------   2 root root  4096 Nov 23  2024 swarm
drwx------   2 root root  4096 Jan  1  1970 tmp
drwx-----x   2 root root  4096 Jan  1  1970 volumes
```

```
sudo du -chs /mnt/nova_ssd/docker/
```

```
59G	/mnt/nova_ssd/docker/
59G	total
```

```
docker info | grep -e "Runtime" -e "Root"
```

```
 Runtimes: io.containerd.runc.v2 nvidia runc
 Default Runtime: nvidia
 Docker Root Dir: /mnt/nova_ssd/docker
```

## Reference

- [Jetson Setup](https://nvidia-isaac-ros.github.io/getting_started/hardware_setup/compute/jetson_storage.html)