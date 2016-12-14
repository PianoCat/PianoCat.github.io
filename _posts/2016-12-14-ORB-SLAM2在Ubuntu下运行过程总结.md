---

layout: post
title: ORB-SLAM2在Ubuntu下运行过程总结
category: SLAM
tags: [SLAM, computer vision, 增强现实, 立体视觉, ROS]
comments: yes

---

之前在实验室的工作有一部分内容是把ORB-SLAM的代码移植到Android端。

现在出了更好的[ORB-SLAM2][1]，这两天把这份代码在Ubuntu14.04上面跑了一下。下面将过程和出现的问题总结一下。

* 准备工作

我的Linux系统是Ubuntu14.04。

首先需要安装和配置以下软件：* Pangolin *, * OpenCV *, * Eigen3 *, * BLAS & LAPACK *, * ROS * 。

安装上面这些包应该都没有太大问题，可以很容易解决。

* 编译ORB-SLAM2

首先下载代码：

```bash
git clone https://github.com/raulmur/ORB_SLAM2.git ORB_SLAM2
```

接下来有两种方法来编译系统：

** 方法一： **

```bash
cd ORB_SLAM2
chmod +x build.sh
./build.sh
```

** 方法二： **

```bash
cd ORB_SLAM2
cd Thirdparty
cd g2o (同理，DBoW2)
mkdir build
cd build
cmake ..
make
```

以上模块只是编译生成了第三方依赖库，接下来是编译主程序：

```bash
cd ORB_SLAM2
mkdir build
cd build
cmake ..
make
```

如果一路顺利的话，ORB-SLAM2已经是编译完毕了，现在就可以跑数据集SLAM了。

* 用摄像头跑在线SLAM

这时候就需要安装ROS系统了。

首先需要将* Examples/ROS/ORB_SLAM2* 添加到ROS_PACKAGE_PATH中(下面export命令中的PATH要换成自己的路径)：

```bash
cd ~
sudo gedit .bashrc
export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:PATH/ORB_SLAM2/Examples/ROS
```

接下来去编译ORB-SLAM2中的ROS模块：

```bash
cd ORB_SLAM2/Examples/ROS/ORB_SLAM2
mkdir build
cd build
cmake .. -DROS_BUILD_TYPE=Release
make -j
```

如果顺利的话，这个模块也编译完成了。但是如果我们要用单目摄像头来调试的话，还需要安装摄像头驱动，如果是USB摄像头，通常需要安装*usb_cam*库，这一部分不再赘述，网上都有安装教程。

安装完之后还需要修改*ORB_SLAM2/Examples/ROS/ORB_SLAM2/src/ros_mono.cc*，其中有一句代码：

```cpp
ros::Subscriber sub = nodeHandler.subscribe("/camera/image_raw", 1, &ImageGrabber::GrabImage,&igb);
```

修改为

```cpp
ros::Subscriber sub = nodeHandler.subscribe("/usb_cam/image_raw", 1, &ImageGrabber::GrabImage,&igb);
```

这里因为usb_cam发布之后的topic是*/usb_cam/image_raw*。

终于可以允许在线单目SLAM了！开启一个终端：

```bash
roscore
```

再开启一个终端：

```bash
cd ~/catkin_ws/src/usb_cam/launch
roslaunch usb_cam-test.launch
```

再开启最后一个终端：

```bash
rosrun ORB_SLAM2 Mono PATH_TO_VOCABULARY PATH_TO_SETTINGS_FILE
```

上面命令中的PATH_TO_VOCABULARY是词典的位置，PATH_TO_SETTINGS_FILE是摄像头标定的yaml文件。这里需要我们事先对自己的摄像头进行标定，按照代码中TUM1.yaml来生成自己的yaml文件，只需要修改其中的内参参数和k1, k2, p1, p2, k3。

以上就是run ORB-SLAM2的所有流程。

下面来说说run的过程中遇到的一些问题：

* 在执行*make*命令的时候报错

```
usr/bin/ld: cannot find -lQt5::Core
usr/bin/ld: cannot find -lQt5::Widgets
usr/bin/ld: cannot find -lQt5::Test
usr/bin/ld: cannot find -lQt5::Concurrent
usr/bin/ld: cannot find -lQt5::OpenGL
```

出现这种错误的解决方法是，在CMakeList.txt中末尾添加：

```
find_package(Qt5Widgets REQUIRED)
find_package(Qt5Test REQUIRED)
find_package(Qt5Concurrent REQUIRED)
find_package(Qt5OpenGL REQUIRED)
```

* 编译ORB-SLAM2中的ROS部分时候报错

```
No rule to make targe ... ' /opencv2.4.8.so ' needed by '...' 
```

用下面这句命令来查看自己系统中的opencv版本：

```bash
pkg-config --modversion opencv 
```

结果显示我的版本是2.4.11啊，但是系统需要2.4.8...这时候我们可以这么做：

```bash
ln -s /usr/local/lib/libopencvxxx2.4.so target_path/lib/libopencvxxx2.4.8.so
```

以上就是对运行在线ORB-SLAM2的一些总结。

[1]: https://github.com/raulmur/ORB_SLAM2