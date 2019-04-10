---
title: UEFI下实现Ubuntu To Go
tags:
  - Ubuntu U盘
  - Ubuntu 便携
abbrlink: be2f0191
date: 2018-09-02 10:00:53
updated: 2018-09-02 10:00:53
---
## 更新历史

- 2018年9月2日：讲解如何U盘中安装UEFI启动的Ubuntu To Go

## 前言

自从Windows To Go(简称WTG)变得越来越普及，于是Ubuntu To Go的尝试也越来越多，总结一下成功的经验。

网上很多介绍Ubuntu To Go的方法都是基于MBR的，个人有需求在一个U盘上（256GB）中同时安装Windows To Go，Ubuntu To Go和黑苹果，MacOS要求必须在GPT分区中使用，所以有了以下的折腾。

## 准备

- 虚拟机VMware Workstation(其它虚拟机如Vitualbox等应该也没问题)
- Ubuntu安装镜像（iso格式，不用解压）
- U盘一只（建议使用固态U盘，随机读写速度是普通U盘几十倍，淘宝搜Windows to go就能找到）
- 提前使用Diskgenius将U盘转为GPT分区，并且新建一个EFI分区，和预留Ubuntu空间（不新建分区）



## 开始

1. 新建一个虚拟机，将默认添加的硬盘删除，具体配置如下图所示。（安装过程选择不自动更新可以加速系统安装）

![](https://ws1.sinaimg.cn/large/d22ff2eely1fuuzgl0gcjj208b08mt8u.jpg)

......
<!-- more --> 

2. 加载U盘到虚拟机中：虚拟机设置-添加-硬盘-SCSI-使用物理磁盘-选择U盘（一般是最后一个），添加后如下图所示。

   ![](https://ws1.sinaimg.cn/large/d22ff2eely1fuuzj70d5zj20kb0jq3ys.jpg)



3. 设置虚拟机为UEFI启动，如下图所示

![。 ](https://ws1.sinaimg.cn/large/d22ff2eely1fuuzkk1bnzj20kb0jqq3r.jpg)

4. 之后启动虚拟机，正常安装Ubuntu，因为VMware软件设计导致Ubuntu显示分辨率低，可以先启动到Ubuntu Live后调整分辨率再启动安装程序，如下图所示。

![](https://ws1.sinaimg.cn/large/d22ff2eely1fuuzs41hklj20sm0nu3yz.jpg)

5. 之后就到了最关键的步骤了：安装完成之后请不要启动Ubuntu启动，先进入Ubuntu Live中。

   5.1 安装grub-efi，打开终端输入

   ```bash
   sudo -s
   apt-get install grub-efi
   ```

   5.2 挂载U盘中的EFI分区和Ubuntu系统分区

   ```bash
   # 查看U盘挂载目录，一般是/dev/sda
   df -l
   mkdir /mnt/EFI
   mkdir /mnt/Ubuntu
   mount /dev/sda1/ /mnt/EFI
   mount /dev/sda2 /mnt/Ubuntu
   ```

   5.3 安装EFI便捷启动到EFI分区

   ```bash
   grub-install --target=x86_64-efi --root-directory=/mnt/EFI/ --efi-directory=/mnt/EFI/Boot
   ```

   5.4 将系统启动文件/mnt/Ubuntu/boot/grub.cfg复制到/mnt/EFI/boot目录下

   5.5 如果便携启动失败，可以尝试启动到系统后安装Grub Customizer，删除启动项后保存，再重复第五部分即可。