# SSD

## SSDデバイスの確認

```
lspci
```

```
0001:00:00.0 PCI bridge: NVIDIA Corporation Device 229e (rev a1)
0001:01:00.0 Network controller: Realtek Semiconductor Co., Ltd. RTL8822CE 802.11ac PCIe Wireless Network Adapter
0004:00:00.0 PCI bridge: NVIDIA Corporation Device 229c (rev a1)
0004:01:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a80c
```

`0004:01:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd Device a80c`がSSD


## マウント先の確認

```
lsblk
```

```
NAME         MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0          7:0    0     4K  1 loop /snap/bare/5
loop1          7:1    0 182.1M  1 loop /snap/chromium/3216
loop2          7:2    0  68.9M  1 loop /snap/core22/2049
loop3          7:3    0  66.6M  1 loop /snap/cups/1102
loop4          7:4    0 493.5M  1 loop /snap/gnome-42-2204/201
loop5          7:5    0  91.7M  1 loop /snap/gtk-common-themes/1535
loop6          7:6    0  42.9M  1 loop /snap/snapd/24787
loop7          7:7    0    16M  1 loop 
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
zram0        252:0    0   3.8G  0 disk [SWAP]
zram1        252:1    0   3.8G  0 disk [SWAP]
zram2        252:2    0   3.8G  0 disk [SWAP]
zram3        252:3    0   3.8G  0 disk [SWAP]
zram4        252:4    0   3.8G  0 disk [SWAP]
zram5        252:5    0   3.8G  0 disk [SWAP]
zram6        252:6    0   3.8G  0 disk [SWAP]
zram7        252:7    0   3.8G  0 disk [SWAP]
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
     ext4   1.0         c1660307-2721-44ef-b1b0-e9f2259dbc86    1.7T     0% /mnt/nova_ssd
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
UUID=c1660307-2721-44ef-b1b0-e9f2259dbc86 /mnt/nova_ssd/ ext4 defaults 0 2
```

## オーナーを変更

```
sudo chown ${USER}:${USER} /mnt/nova_ssd
```
