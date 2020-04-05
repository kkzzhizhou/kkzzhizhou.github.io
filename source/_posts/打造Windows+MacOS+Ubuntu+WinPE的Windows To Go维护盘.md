---
title: 打造Windows+Mac OS X+Ubuntu+WinPE的Windows To Go维护U盘
tags: 多功能U盘
abbrlink: multiboot-wtg
date: 2017-12-16 00:00:00
updated: 2020-3-16 13:36:57
---

## 前言

![multiboot-wtg-1.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-1.png)

作为一个极客，随便带一个维护PE的U盘是必需的。然而在很多时候，仅仅有一个PE，难以完成复杂的需求。我手头上有一个128G的Windows To Go U盘，想为别人安装Ubuntu时，必须要拿另外一个U盘全盘格式化后写入，麻烦，而且也浪费资源。所以这次写一篇关于U盘多启动的文章，实现标题的中效果。

<!-- more -->
  
## 准备工作
  你得有一个不小于64GB的Windows To Go U盘。
  使用到的软件：
  1. DiskGenius(或PartitionGuru)
  2. UEFI启动修复工具
  3. XYplorer
  4. Vmware Pro
  5. Bootice
  6. Dism++

  使用到的镜像：
  1. Ubuntu 16.04.3安装镜像
  2. Mac OS X 13.1安装镜像(dmg格式)
  3. 微PE
  4. Windows 10 1709企业版镜像

## 开始折腾
  1. 这次使用到的启动方式为GPT+EFI（使用PartitionGuru软件进行操作）。如果对启动方式不了解，在这里简单的科普一下，有两种启动方式，一种是BIOS+MBR，一种是GPT+EFI，前者复杂，后者简单。
  2. 进行分区操作，350MB的EFI（ESP）启动分区，5.5GB的FAT32分区（只是暂时，稍后需要在苹果系统中格式化为HFS+分区），2GB的FAT32分区用于放Ubuntu 16.04.3的安装镜像，500MB的FAT32分区用于PE（只装一个PE的话600MB即可），以及最后10的空间格式化为NTFS分区用于Windows To Go的系统及软件。
  PS:**前四个分区设置了隐藏，在电脑中不可见，不然一插进电脑就出来5个盘，不美观也不实用。**
  
![multiboot-wtg-2.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-2.png)


## EFI分区
这个分区的用途是用于搜索和引导其他分区上的安装镜像和系统。 使用到的引导管理工具为rEFInd（主要）和Clover（黑苹果安装辅助）。关于引导管理工具的使用，这里只简单提一点：开机时进入的EFI文件是在/EFI/Boot/下。

![multiboot-wtg-3.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-3.png)


## 写入苹果安装镜像
在虚拟机中安装苹果操作系统，具体的操作见[简书-Hegel_SU](http://www.jianshu.com/p/25d2d781bd98)的文章。

![multiboot-wtg-4.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-4.png)

打开苹果的操作系统，插入U盘，磁盘工具，将5.5GB的FAT32分区格式化为HFS+分区。之后用命令行写入苹果镜像。

![multiboot-wtg-5.jpg](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-5.jpg)

命令行写入苹果DMG镜像教程：[iplaysoft](https://www.iplaysoft.com/macos-usb-install-drive.html)

![multiboot-wtg-6.jpg](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-6.jpg)

## 写入Ubuntu系统镜像
将安装镜像解压至2GB的FAT32分区中，同时删除该分区目录/EFI/Boot/Bootx64.EFI即可

![multiboot-wtg-7.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-7.png)

## 写入微PE工具箱
准备另一个8GB的文章，打开微PE工具箱写入程序，选择方案二：UEFI/Legacy全能双分区方式，写入后在隐藏的引导分区中提取WEPE64.WIM，WEPE64.SDI和引导文件/EFI/Microsoft下的文件到500MB的FAT32分区中。

![multiboot-wtg-8.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-8.png)

![multiboot-wtg-9.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-9.png)

## 安装完整的Windows to go-Win10系统
在Windows下创建一个VHD文件（建议20GB）放到最后一个分区NTFS中，（科普一下，VHD指的是Vitual Hard Disk即虚拟硬盘文件），挂载VHD后在DiskGenius中格式化VHD文件，然后用Dism++以Windows To Go方式写入Windows 10的系统镜像，之后在U盘的EFI分区中，用Bootice修复Windows 10的引导。

![multiboot-wtg-10.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-10.png)

![multiboot-wtg-11.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-11.png)

![multiboot-wtg-12.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-12.png)

![multiboot-wtg-13.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-13.png)

![multiboot-wtg-14.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-14.png)

![multiboot-wtg-15.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/multiboot-wtg-15.png)


## 结束语

至此，一个多功能U盘打造完成，前前后后折腾了两天多，茶不思饭不想，如果你也非常想要达到这样的目的，请做好心想准备，过程将会非常的闹心,Good luck。