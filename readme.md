# 前言

为了提高一下自己的编程能力，同时觉得用python写的人脸识别代码在使用时并不够高效和快速。python编写ros同时缺失了相当一部分的功能所以利用空闲时间编写一下新的人脸识别代码。

# 准备
1. ros服务的cpp基本框架

1. realsense相机的cpp使用方式

1. cpp语言编写程序的规范化写法

1. 人脸识别代码库的安装与使用

1. 顺便锻炼一下刚学的git的使用能力

1. 同时现学现用一下ssh

# 详细步骤

## ros服务基本框架构建

提供的服务客户端代码示例:

```cpp
/**
 * 该例程将请求/show_person服务，服务数据类型learning_service::Person
 */
#include <ros/ros.h>
#include "learning_service/Person.h"

int main(int argc, char** argv)
{
    // 初始化ROS节点
        ros::init(argc, argv, "person_client");

    // 创建节点句柄
        ros::NodeHandle node;

    // 发现/spawn服务后，创建一个服务客户端，连接名为/spawn的service
        ros::service::waitForService("/show_person");
        ros::ServiceClient person_client = node.serviceClient<learning_service::Person>("/show_person");

    // 初始化learning_service::Person的请求数据
        learning_service::Person srv;
        srv.request.name = "Tom";
        srv.request.age  = 20;
        srv.request.sex  = learning_service::Person::Request::male;

    // 请求服务调用
        ROS_INFO("Call service to show person[name:%s, age:%d, sex:%d]",
                         srv.request.name.c_str(), srv.request.age, srv.request.sex);

        person_client.call(srv);

        // 显示服务调用结果
        ROS_INFO("Show person result : %s", srv.response.result.c_str());

        return 0;
};
```
提供的cpp服务服务端示例:
```cpp
/**
 * 该例程将执行/show_person服务，服务数据类型learning_service::Person
 */

#include <ros/ros.h>
#include "learning_service/Person.h"

// service回调函数，输入参数req，输出参数res
bool personCallback(learning_service::Person::Request  &req,
                                learning_service::Person::Response &res)
{
    // 显示请求数据
    ROS_INFO("Person: name:%s  age:%d  sex:%d", req.name.c_str(), req.age, req.sex);

        // 设置反馈数据
        res.result = "OK";

    return true;
}

int main(int argc, char **argv)
{
    // ROS节点初始化
    ros::init(argc, argv, "person_server");

    // 创建节点句柄
    ros::NodeHandle n;

    // 创建一个名为/show_person的server，注册回调函数personCallback
    ros::ServiceServer person_service = n.advertiseService("/show_person", personCallback);

    // 循环等待回调函数
    ROS_INFO("Ready to show person informtion.");
    ros::spin();

    return 0;
}
```

## realsense相关配置
~~1. 像使用pyrealsense一样在cpp下使用realsense我们也需要相应的库这里使用的是[librealsense](https://github.com/IntelRealSense/librealsense/)~~

1. 并非如此!!!如果你有ros那麽一切都好办了，你只需要用下面的两条指令就能够安装librealsense。（下次在安装驱动时记得看看有没有ros特供版!!!）
```shell
sudo apt-get install ros-noetic-realsense2-camera
sudo apt-get install ros-noetic-realsense2-description
```