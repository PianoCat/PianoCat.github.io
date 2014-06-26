## 安装Ubuntu前后 ##

#### 1.关于安装 ####

安装*linux*系统我一向用的是*Ultra ISO*这个工具，通过这个工具做一个U盘启动，然后从U盘安装。记得以前安装时候要设置启动U盘为USB-HDD，这次安装14.04*x*64版本时候这样设置制作U盘启动不能成功，只能设置为USB-ZIP才行。之后的安装就一路顺利了。

#### 2.Flash player的安装 ####

每次装完系统，第一件要干的事情就是让系统能播放网上视频。这是安装*Flash player*的代码：`sudo apt-get install flashplugin-installer`，这件事情就轻松搞定啦！

#### 3.安装qq ####

每次开电脑都离不开qq啊，保持和外界的沟通。*linux*下qq一直太弱，用*web qq*也很不爽。。还好*wine qq*可以轻松搞定！只需要从[这里](http://www.longene.org/download/WineQQ2013SP6-20140102-Longene.deb)下载，使用`sudo apt-get install libgtk2.0-0:i386`命令解决所有依赖，再用命令`sudo dpkg -i 软件名.deb`安装即可。在64位系统下有三个bug，大部分时候不能使用qq表情；与输入法不是很兼容；登录输入密码时候可能需要用到旁边软键盘。

#### 4.更换默认启动的系统 ####

我的电脑是win8x64和Ubuntu14.04共存。在家时候老妈有时候想玩会儿qq升级游戏，开机时候不知道要选择windows进入，于是我就帮她方便方便吧：

1. `sudo gedit /boot/grub/grub.cfg`，设置默认选项为4，也就是windows那项；
2. `sudo update-grub`

这样以后默认进入的就是windows啦！


至于最快的源神马的，我觉得默认就挺快的，就先做这些事情吧~~