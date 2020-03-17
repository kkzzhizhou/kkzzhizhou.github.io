---
title: Windows中硬链接、软链接、符号链接区别与使用场景
comments: true
date: 2020-03-17 17:35:30
updated: 2020-3-17 18:25:57
tags: 
- 文件系统
categories: 
- [Windows]
abbrlink: windows-links
---

## 概念

- 硬链接：Hard Link, 只适用于文件
适用条件：NTFS文件系统,不能跨盘符,使用绝对路径
使用效果：硬链接文件与目标文件必须位于同一volume,删除硬链接文件，不影响目标文件,删除目标文件，不影响硬链接文件(此时硬链接会保留目标文件的副本),当移动目标文件时，硬链接会重新指向新路径。

- 软链接：只用适用于目录
适用条件：NTFS文件系统,不能跨主机,使用绝对路径
使用效果：删除软链接，不影响目标文件夹,删除目标文件夹，软链接失效

- 符号链接：支持目录和文件
适用条件：NTFS文件系统，支持相对路径,支持UNC路径、网络驱动器。
使用效果：删除符号链接(文件或者目录)，不影响目标(文件或者目录),删除目标(文件或者目录),符号链接失效

<!-- more --> 

## CMD实现

``` batch
; 创建硬链接
mklink /H 硬链接文件 目标文件
; 创建软链接
mklink /j 软链接文件夹 目标文件夹
; 创建符号链接
mklink 符号链接文件或文件夹 目标文件或文件夹
```

## PowerShell实现

```
# 创建硬链接
New-Item -ItemType HardLink -Path 硬链接文件所在目录 -Name 硬链接文件名 -Target 目标文件全路径"
# 创建软链接
New-Item -ItemType Junction -Path 软链接文件夹 -Value 目标文件夹
# 创建符号链接
New-Item -ItemType SymbolicLink -Path 符号链接文件或文件夹  -Value 目标文件或文件夹
```

## 使用案例

- 硬链接：在scoop包管理器中大量使用,个人不常用
- 软链接：在不改变配置的情况下，将文件夹同步至OneDrive
- 符号链接：在不改变配置的情况下，将文件同步至OneDrive