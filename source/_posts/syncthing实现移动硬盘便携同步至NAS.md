---
title: syncthing实现移动硬盘便携同步至NAS
date: 2020-03-13 17:22:17
updated: 2020-03-13 17:22:17
tags:
categories:
comments: true
abbrlink: Synchronize-Portable-External-Hard-Drive-With-NAS
---

## 需求

一台黑群晖NAS设备和一个移动硬盘实现在资料自动同步

先说说传统方式有几种：

- 将移动硬盘插入NAS的USB接口，并使用群晖应用USB Copy进行备份(注意：这种方式只能备份至移动硬盘，不能将移动硬盘上的更改同步到NAS中)
- 将移动硬盘插入局域网中的Windows设备，并使用samba挂载NAS文件夹，使用类似GoodSync，AllwaySync，SyncFolders等同步软件进行同步。

我的需求：

- 移动硬盘接入任何Windows设备中，在有网络的情况下（可以是局域网，可以是公网），都能直接与NAS中的文件夹进行同步。
- 即使移动硬盘在一段时间内不使用（比如说，不接任何设备闲置几天），重新接入网络能继续与NAS中的文件夹进行同步

## 可行解决方案：SyncTrayzor(Syncthing GUI)

......
<!-- more --> 

## 实现方式

1. 下载SyncTrayzor Portable版本，解压放置在移动硬盘根目录，命名为Syncthing(可以改成任何你想到的名字)

2. 将硬盘盘符修改成一些不常用的的盘符，比方说P盘
3. 打开Syncthing文件夹中的SyncTrayzor.exe，将设备名改成移动硬盘的盘符名（最好是有意义的）
4. 添加远程设备NAS，去除勾选“作为中介”
5. 将移动硬盘中的文件夹同步给ZNAS即可

## 插入新设备时

- 修改移动硬盘盘符为P盘（或者修改配置文件中的[盘符]:\Syncthing\data\syncthing\config.xml中的盘符位置)
- 打开SyncTrayzor即可同步

## 自动修改盘符脚本

- 将以下代码保存成start.ps1后打开即可

``` powershell
$script_path = Split-Path -Parent $MyInvocation.MyCommand.Definition
$config = "$script_path\data\syncthing\config.xml"
$drive_letter = $script_path.Split('\')[0]

write-host "正在修改盘符..." 
$xml = New-Object -TypeName XML
$xml.Load($config)
$node=$xml.SelectNodes("/configuration/folder")
write-host "旧盘符为:${node.path}" 
$node.SetAttribute("path", $drive_letter)
write-host "新盘符为:$drive_letter"
$xml.Save($config)

if($?){
    write-host "正在启动SyncTrayzor"
    Start-Process $script_path\SyncTrayzor.exe
}
```



