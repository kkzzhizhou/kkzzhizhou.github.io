---
title: USBIP实现路由器连接打印机，可打印可扫描
tags:
  - usbip
categories:
  - openwrt
abbrlink: bd0d1da
date: 2017-08-26 00:00:00
updated: 2017-08-26 00:00:00
---

## 前言
众所周知，智能路由器的USB接口能够连接打印机，让没有网络功能的路由器实现网络打印。可惜的是，打印机连接路由器后提只能打印不能扫描，这很不方便。在寻找中发现一项**USB over IP** 技术（又称 USB over Ethernet 或者 USB over Internet），这个技术能够解决以上的问题，并能扩展出不少应用场景。
<!-- more --> 
## USB over IP简介

按照[官网][1]的描述，这个技术解决的问题是跨设备跨平台通过网络共享同一个USB设备。简单的理解就是，USB设备接在你的电脑上，我通过网络设备就是访问到该USB设备，就好像这个USB设备直接接在我的电脑上一样。

相关视频教程：
[youtube:USB over Ethernet: Share USB devices over Ethernet][2]

## 实验环境

路由器：优酷土豆YK-L1(**CPU：mt7620a，路由器配置软件源只跟CPU有关**)
路由器操作系统：Pandorabox（**基于openwrt 14.09 Barrier Breaker** ）
打印机：三星SCX-3400系列（打印扫描复印一体机）
Windows平台：Win10

## 步骤简介
1. 让路由器刷上基于openwrt的固件（如pandarobox）。[下载地址][3]
    注：如果路由器还没有刷Uboot，请先刷Uboot，再通过Uboot刷Openwrt固件。
2. 配置Pandorabox软件源，在**系统--软件包--配置**中填入后提交
	**注：此软件源适用于mt7620a/n路由器，如果你的路由器不是此CPU，请自行查找软件源。**
``` stylus
dest root /
dest ram /tmp
lists_dir ext /var/opkg-lists
option overlay_root /overlay
src/gz r2_base http://downloads.openwrt.org.cn/PandoraBox/ralink/packages/base
src/gz r2_management http://downloads.openwrt.org.cn/PandoraBox/ralink/packages/management
src/gz r2_oldpackages http://downloads.openwrt.org.cn/PandoraBox/ralink/packages/oldpackages
src/gz r2_packages http://downloads.openwrt.org.cn/PandoraBox/ralink/packages/packages
src/gz r2_routing http://downloads.openwrt.org.cn/PandoraBox/ralink/packages/routing
src/gz r2_telephony http://downloads.openwrt.org.cn/PandoraBox/ralink/packages/telephony
src/gz r2_oldpackages2 http://downloads.openwrt.org.cn/PandoraBox/ralink/mt7620_old/packages
src/gz 16.10_base http://downloads.pandorabox.com.cn/pandorabox/packages/mt7620/packages/base
src/gz 16.10_luci http://downloads.pandorabox.com.cn/pandorabox/packages/mt7620/packages/luci
src/gz 16.10_packages http://downloads.pandorabox.com.cn/pandorabox/packages/mt7620/packages/packages
```
3. 使用putty连接路由器，[使用教程][4]。**注：用户名：root，密码默认是admin**
4. 在路由器上安装USBIP软件包。[英文教程][5]，[英文教程2][6]
	注：**在使用过程中会报错：error: please load usbip-core.ko and usbip-host.ko!**
    解决方法：终端输入
``` crystal
	insmod /lib/modules/3.2.0-24-generic/kernel/drivers/staging/usbip/usbip-core.ko 
	insmod /lib/modules/3.2.0-24-generic/kernel/drivers/staging/usbip/usbip-host.ko
```
   安装测试成功后可接相关指令放入**系统-启动项-本地启动脚本**添加命令后提交。
5. 以上步骤已经把路由器端的软件安装配置好了，测试是否正常工作的方法是看以下命令是否正常运行

``` stylus
usbip list -l
usbipd -D & usbip bind -b 1-1
netstat -alpt |grep usbipd
```
6. 以下步骤是在Windows平台上操作。下载usbip_windows_v0.2.0.0_signed[usbip下载][7]
7. 解压后安装驱动，打开设备管理员--选择此电--操作--添加过时硬件--从磁盘中安装。
	**注：如果无法正常安装，请用管理员权限打开命令行输入：bcdedit /set testsigning on**
8. 安装成功能，用bat命令行（批处理运行）usbip.exe程序（**该程序没有用户界面，只有命令行。**），在解压路径中打开命令行，输入以下命令：
``` stylus
usbip -h //查看帮助
usbip -l 192.168.1.1 //查看路由器上连接的USB设备
usbip -a 192.168.1.1 1-1  //连接到路由器的BUS 1-1
```
	**注：可能遇到的问题：**
	usbip err: usbip_network.c: 121 (usbip_recv_op_common) recv op_common,-1 usbip err: 	usbip_windows.c: 756 (query_interface0) recv op_common 
	usbip err: usbip_windows.c: 829 (attach_device) cannot find device
	
	解决方法：下载这个去BUG版本的usbip程序。[下载地址][8]

9. 已经以上步骤连接成功后就可以正常使用了。连接成功提示如下：
``` stylus
new usb device attached to usbvbus port 1
```
	成功后，电脑会自动安装相应的驱动程序。Enjoy!

## 应用场景
除了以上共享打印机，扫描仪，还可以共享摄像头，共享3G无线网卡实现多人分享上网。
[相关介绍][9]


[1]: http://usbip.sourceforge.net/
[2]: https://www.youtube.com/watch?v=vGBWZzXx2KM
[3]: http://downloads.pandorabox.com.cn/pandorabox/
[4]: https://jingyan.baidu.com/article/90808022f011c5fd91c80f91.html
[5]: https://wiki.openwrt.org/doc/howto/usb.iptunnel
[6]: http://www.madox.net/blog/2013/01/04/tl-wr703n-example-project-3-wireless-3d-printing-or-2d-printing-or-just-simply-wireless-usb/
[7]: https://sourceforge.net/projects/usbip/
[8]: https://www.dropbox.com/s/oox021z1d7zblmu/usbip.zip?dl=0
[9]: http://www.wikidrv.cn/index.php?m=content&c=index&a=show&catid=14&id=116