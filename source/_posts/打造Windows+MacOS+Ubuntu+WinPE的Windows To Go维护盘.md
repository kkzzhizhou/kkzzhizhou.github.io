---
title: 打造Windows+Mac OS X+Ubuntu+PE的Windows To Go维护U盘
date: 2017-12-16
updated: 2017-12-16
tags: 多功能U盘
---
  作为一个极客，随便带一个维护PE的U盘是必需的。然而在很多时候，仅仅有一个PE，难以完成复杂的需求。我手头上有一个128G的Windows To Go U盘，想为别人安装Ubuntu时，必须要拿另外一个U盘全盘格式化后写入，麻烦，而且也浪费资源。所以这次写一篇关于U盘多启动的文章，实现标题的中效果。
  
##  折腾之后的效果图
  由图中可以看到，启动菜单有Windows To Go完整的操作系统，Mac OS X的安装盘，Ubuntu的安装盘，以及一个PE，还有一个Clover的启动工具。

![效果图][1]
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
  
  ![分区展示][2]
  
## EFI分区
这个分区的用途是用于搜索和引导其他分区上的安装镜像和系统。 使用到的引导管理工具为rEFInd（主要）和Clover（黑苹果安装辅助）。关于引导管理工具的使用，这里只简单提一点：开机时进入的EFI文件是在/EFI/Boot/下。

![EFI分区][3]

## 写入苹果安装镜像
在虚拟机中安装苹果操作系统，具体的操作见[简书-Hegel_SU][4]的文章。

![虚拟机安装Mac OS X][5]

打开苹果的操作系统，插入U盘，磁盘工具，将5.5GB的FAT32分区格式化为HFS+分区。之后用命令行写入苹果镜像。

![格式化为HFS+分区图例][6]

命令行写入苹果DMG镜像教程：[iplaysoft][7]

![命令行][8]

## 写入Ubuntu系统镜像
将安装镜像解压至2GB的FAT32分区中，同时删除该分区目录/EFI/Boot/Bootx64.EFI即可

![Ubuntu镜像文件][9]



## 写入微PE工具箱
准备另一个8GB的文章，打开微PE工具箱写入程序，选择方案二：UEFI/Legacy全能双分区方式，写入后在隐藏的引导分区中提取WEPE64.WIM，WEPE64.SDI和引导文件/EFI/Microsoft下的文件到500MB的FAT32分区中。

![微PE工具箱][10]

![方案二][11]

## 安装完整的Windows to go-Win10系统
在Windows下创建一个VHD文件（建议20GB）放到最后一个分区NTFS中，（科普一下，VHD指的是Vitual Hard Disk即虚拟硬盘文件），挂载VHD后在DiskGenius中格式化VHD文件，然后用Dism++以Windows To Go方式写入Windows 10的系统镜像，之后在U盘的EFI分区中，用Bootice修复Windows 10的引导。

![VHD][12]

![格式化VHD文件][13]

![释放Win10镜像][14]

![释放Windows镜像][15]

![修改BCD文件][16]

![修改启动项][17]


## 结束语
至此，一个多功能U盘打造完成，前前后后折腾了两天多，茶不思饭不想，如果你也非常想要达到这样的目的，请做了心思准备，过程将会非常的虐心。Good luck。
  
  


  [1]: https://lh3.googleusercontent.com/-VHXDITij1U4/WjX882g5SxI/AAAAAAAAc6I/oUUlxyU13ZYLiSKMvdkpwMnDNjVhN57BwCHMYCw/s0/2017-12-17_13-13-21.png
  [2]: https://lh3.googleusercontent.com/-xAksKBeKbuo/WjX888TMI1I/AAAAAAAAc6E/piII0_swKFYX1J3vIIdwYXUGfsHHEmJ5gCHMYCw/s0/2017-12-17_13-13-21.png
  [3]: https://lh3.googleusercontent.com/-TjcIZ03EEKs/WjX9uTLZwYI/AAAAAAAAc6Q/sVrV4DHV03EMRbzVvdp37_atvYcNtmi3ACHMYCw/s0/2017-12-17_13-16-43.png
  [4]: http://www.jianshu.com/p/25d2d781bd98
  [5]: https://lh3.googleusercontent.com/-qQW-kaUtIGQ/WjX9-F7ub9I/AAAAAAAAc6U/iH0pj9k9vN4T8JMvBymOJy2dgH3XUpUUgCHMYCw/s0/2017-12-17_13-17-46.png
  [6]: https://lh3.googleusercontent.com/-K6TATgCwks4/WjX-Rtob8hI/AAAAAAAAc6c/UfzqSKTzchsd9kvGbc44PMm_Mu21Vd01gCHMYCw/s0/2017-12-17_13-19-04.jpg
  [7]: https://www.iplaysoft.com/macos-usb-install-drive.html
  [8]: https://lh3.googleusercontent.com/-ZRra0P83Ztc/WjX-f8FUZ1I/AAAAAAAAc6g/xW7_sh8qWnMWD8vIVXjTpD-Ow1h4NsNYACHMYCw/s0/2017-12-17_13-20-01.jpg
  [9]: https://lh3.googleusercontent.com/-kmfgxrIvKec/WjX-zBBSqJI/AAAAAAAAc6o/zX2xiD-VZgodJXY4Q4cUn_lt9OSAEKciACHMYCw/s0/2017-12-17_13-21-18.png
  [10]: https://lh3.googleusercontent.com/-SxRPXXBvQPE/WjX_Y5rrfHI/AAAAAAAAc60/9Ec9eanEFREjW76xD4YmGAA1uFvIfQY9wCHMYCw/s0/2017-12-17_13-23-48.png
  [11]: https://lh3.googleusercontent.com/-L3PijYqVTVw/WjX_fWiIbMI/AAAAAAAAc64/EQrb9-ZUqYgPGm02xf0pHGarVdJEs_SPQCHMYCw/s0/2017-12-17_13-24-15.png
  [12]: https://lh3.googleusercontent.com/-wniNbJcPgA8/WjYAAl0BlRI/AAAAAAAAc7A/ek3de8BYijwAoOdpPF-ezv1p3nnh0xzVACHMYCw/s0/2017-12-17_13-26-27.png
  [13]: https://lh3.googleusercontent.com/-VrBbHFks_0U/WjYAQ1FGSWI/AAAAAAAAc7E/g8gAns3LIykjtohp14gHGPcA5gn0coc1wCHMYCw/s0/2017-12-17_13-27-33.png
  [14]: https://lh3.googleusercontent.com/-NlhQv3N7zYY/WjYAfyfggBI/AAAAAAAAc7I/ubRwKrfcU2oDXqx65QlR188WASPo1qPFQCHMYCw/s0/2017-12-17_13-28-33.png
  [15]: https://lh3.googleusercontent.com/-vk_Tt2wbHhc/WjYA1zuuh-I/AAAAAAAAc7U/03WEQF3TysMBMSfA3hmrGUYZU5VyWz2hQCHMYCw/s0/2017-12-17_13-30-01.png
  [16]: https://lh3.googleusercontent.com/-Pfx5ens64xw/WjYBKWmuOOI/AAAAAAAAc7Y/Kp4I0-AmKw0rgAJZ5TsG0iXFsIT2bjwrACHMYCw/s0/2017-12-17_13-31-23.png
  [17]: https://lh3.googleusercontent.com/-Dx_3HW7Z7X4/WjYBhlbFlTI/AAAAAAAAc7g/Tf1SN8m1rUUjzzaQR1xd7iXQ18mfDT8dwCHMYCw/s0/2017-12-17_13-32-56.png