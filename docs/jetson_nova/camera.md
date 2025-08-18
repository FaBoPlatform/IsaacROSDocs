# Nova Orin搭載カメラ

!!!Info
    Jetson Orin Nova Developer KitではGMSL2でカメラの接続をおこなっています。内部的にはCSI同様に認識でき、nvarguscameraからアクセス可能になります。GPUへ直接展開可能となり、カメラ映像での低遅延での転送や、同期を実現しています。

## Depthカメラ

|型番|メーカー|端子|データシート|
|:--|:--|:--|:--|
|[LI-AR0234CS-STEREO-GMSL2-30](https://leopardimaging.com/product/automotive-cameras/cameras-by-interface/maxim-gmsl-2-cameras/li-ar0234cs-stereo-gmsl2/li-ar0234cs-stereo-gmsl2-30/)|LEOPARD imaging|GMSL2|[Datasheet](https://leopardimaging.com/wp-content/uploads/2024/07/LI-AR0234CS-STEREO-GMSL2-30_Datasheet_V1.8.pdf)|

## Hawkカメラ

|型番|メーカー|端子|データシート|
|:--|:--|:--|:--|
|[LI-AR0234CS-GMSL2-OWL](https://leopardimaging.com/product/automotive-cameras/cameras-by-interface/maxim-gmsl-2-cameras/li-ar0234cs-gmsl2-owl/li-ar0234cs-gmsl2-owl/)|LEOPARD imaging|GMSL2|[Datasheet](https://leopardimaging.com/wp-content/uploads/2023/12/LI-AR0234CS-GMSL2-OWL_Datasheet.pdf)|

## GMSL変換基板

|型番|メーカー|用途|
|:--|:--|:--|
|[LI-JAG-ADP-GMSL2-8CH](https://leopardimaging.com/product/accessories/adapters-carrier-boards/for-nvidia-jetson/li-jag-adp-gmsl2-8ch/)|LEOPARD imaging|LI-AR0234CS-STEREO-GMSL2-30用|


## Reference

- [Isaac ROS Hawk Setup](https://nvidia-isaac-ros.github.io/getting_started/hardware_setup/sensors/hawk_setup.html)
