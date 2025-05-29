# 前言

为了提高一下自己的编程能力，同时觉得用python写的人脸识别代码在使用时并不够高效和快速。python编写ros同时缺失了相当一部分的功能所以利用空闲时间编写一下新的人脸识别代码。

# 准备

1. realsense相机的cpp使用方式

1. cpp语言编写程序的规范化写法

1. 人脸识别代码库的安装与使用

1. 顺便锻炼一下刚学的git的使用能力

1. 同时现学现用一下ssh

# 详细步骤

## realsense相关配置
~~1. 像使用pyrealsense一样在cpp下使用realsense我们也需要相应的库这里使用的是[librealsense](https://github.com/IntelRealSense/librealsense/)~~

1. 并非如此!!!如果你有ros那麽一切都好办了，你只需要用下面的两条指令就能够安装librealsense。（下次在安装驱动时记得看看有没有ros特供版!!!）
```bash
sudo apt-get install ros-noetic-realsense2-camera
sudo apt-get install ros-noetic-realsense2-description
```