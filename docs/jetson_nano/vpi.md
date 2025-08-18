# VPI

Jetson VPI（Vision Programming Interface）は、NVIDIA Jetsonシリーズ向けの画像・映像処理用ライブラリです。
NVIDIAが提供しており、GPUやPVA（Programmable Vision Accelerator）、VIC（Video Image Compositor）といったJetsonの専用ハードウェアを活用して、高速かつ省電力にコンピュータビジョン処理を実行できます。

## GPUデバイス情報（CDI spec）を作成

```
sudo nvidia-ctk cdi generate --mode=csv --output=/etc/cdi/nvidia.yaml
```

## パッケージのインストール

```
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-key adv --fetch-key https://repo.download.nvidia.com/jetson/jetson-ota-public.asc
sudo add-apt-repository 'deb https://repo.download.nvidia.com/jetson/common r36.4 main'
sudo apt-get update
sudo apt-get install -y pva-allow-2
```