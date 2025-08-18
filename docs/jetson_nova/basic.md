# Orin Nova基本情報

!!!Info
    Jetson Orin Nova Developer Kitの初期はJetPack6.1対応でしたが、現在はJetPack6.2に対応しています。JetPack6.2.1にアップデートをするとデバイス周りのドライバーが対応していない可能性がありますので、JetPack6.2での動作をおすすめします。

## ログイン画面

```
Welcome to Ubuntu 22.04.4 LTS (GNU/Linux 5.15.148-tegra aarch64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

Expanded Security Maintenance for Applications is not enabled.

687 updates can be applied immediately.
269 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

82 additional security updates can be applied with ESM Apps.
Learn more about enabling ESM Apps service at https://ubuntu.com/esm


The list of available updates is more than a week old.
To check for new updates run: sudo apt update
Last login: Mon Mar 17 15:35:45 2025 from 192.168.128.123
               =======================  OS: Ubuntu 22.04 jammy
               -======================  Kernel: aarch64 Linux 5.15.148-tegra
          --==-       --==============  Uptime: 2m
      -==-     =====-     -===========  Shell: bash 5.1.16
   -==-     ===    -===-    -=========  Disk: 136G / 1.9T (8%)
 ===-    ===-  -      -==-    ========  CPU: ARMv8 rev 1 (v8l) @ 12x 2.2016GHz
 ===   -==-    ===    ===     ========  GPU: Orin (nvgpu)
  ===   -==    ========-    ====--====  RAM: 3227MiB / 62840MiB
   ===-   ==-  =====-    -===-      -=  Nova Config: nova-devkit
    -===    -=-       -===-         ==  Nova Version: 1.3.2+b4
      -===-    =======--        -=====  Jetpack: 6.2+b77
         -====-            -========== 
               ======================= 
               ======================= 
```

## 各種バージョン

|項目|バージョン|
|:--|:--|
|OS|Ubuntu 22.04|
|Kernel|aarch64 Linux 5.15.148-tegra|
|JetPack|6.2|


## /etc/nv_tegra_release

```
# R36 (release), REVISION: 4.0, GCID: 37537400, BOARD: generic, EABI: aarch64, DATE: Fri Sep 13 04:36:44 UTC 2024
# KERNEL_VARIANT: oot
TARGET_USERSPACE_LIB_DIR=nvidia
TARGET_USERSPACE_LIB_DIR_PATH=usr/lib/aarch64-linux-gnu/nvidia
```

## apt policy nova-orin-init

```
apt policy nova-orin-init
```

```
nova-orin-init:
  Installed: 1.3.2+b4
  Candidate: 1.3.2+b4
  Version table:
 *** 1.3.2+b4 600
        600 https://isaac.download.nvidia.com/nova-init jammy/main arm64 Packages
        100 /var/lib/dpkg/status
     1.3.2+b3 600
        600 https://isaac.download.nvidia.com/nova-init jammy/main arm64 Packages
     1.3.1 600
        600 https://isaac.download.nvidia.com/nova-init jammy/main arm64 Packages
     1.3.0 600
        600 https://isaac.download.nvidia.com/nova-init jammy/main arm64 Packages
```

