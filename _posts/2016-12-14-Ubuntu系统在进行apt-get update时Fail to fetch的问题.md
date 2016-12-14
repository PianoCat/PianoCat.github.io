---
layout: post
title: ORB-SLAM2在Ubuntu下运行过程总结
category: SLAM
tags: [SLAM, computer vision, 增强现实, 立体视觉, ROS]
comments: yes

---



之前在运行` sudo apt-get update`命令时老是会出错：



```bash
W: Failed to fetch http://mirrors.ustc.edu.cn/ubuntu/dists/trusty/Release  Unable to find expected entry 'main/binary-i386sudo/Packages' in Release file (Wrong sources.list entry or malformed file)  
...
...
```



刚开始以为是源的问题，后来换了几次也还是没用。后来仔细分析这些错误，发现`i386sudo`是个什么鬼！Google一下，也有人是出现`binary-i38`的问题。。就不知道这些残缺的命名是怎么来的。最终还是找到了解决办法：



```bash
dpkg --print-foreign-architectures
> i386
> i386sudo
```



删除这个`i386sudo`就好了！



```sudo
dpkg --remove-architecture i386sudo
```

