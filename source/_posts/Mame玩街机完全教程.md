---
title: Mame玩街机完全教程
date: 2017-4-5
updated: 2020-3-16 15:42:39
tags:
  - mame
  - 街机
abbrlink: mame-tutorial
---

## 街机模拟器的选择
网上有很多类型的街机模拟器,如比较知名的mame及其分支（mameplus,mame plus! plus!,mame32 more等），winkawaks，fba shuffle ,nebula(星云模拟器)等等。

想要实现标题中所提到的所有功能，请使用**mame32 more**（联机对战）或者**mame plus! plus!**（两个版本集成联机对战功能）

我的选择：**mame32 more**
<!-- more --> 
## 街机模拟器下载

1. [mame32 more](https://emulationrealm.net/downloads/file/3169-mame32-more)
2. [mame plus! plus!](http://www.zophar.net/mame/mame32-plus-plus.html)

## BIOS及游戏ROM下载

科普：好多游戏都需要有BIOS文件的支持才能运行，比如NEOGEO的游戏都需要neogeo.zip这个BIOS文件才能玩，如果没有，MAME是不会认NEOGEO的游戏的。
BIOS不需要一个一个下，直接下一个游戏合集包，在模拟器\roms目录下（可能会隐藏）。
游戏包：http://www.game333.net/danji/oth/329677.html
游戏ROM及BIOS下载网站：
1. http://www.doperoms.com/  （这个网站收录了大部分的游戏及全部的BIOS,某些盗版的rom没有。）
2. http://www.romnation.net/ 

## 联机对战（2017年4月5日更新）
联机对战使用到kaillera，在文件 -> play kaillera game
1. 点对点模式最多支持两个人（或者说两台电脑）同时联机
2. 联机模式可支持2人以上同时进行游戏，比如说恐龙新世纪3人联机，三国战纪4人联机。

3人至多人联机教程，简单的就以恐龙快打为例：
1. 局域网中需要有一台电脑用**KaillerasrvGUI**建立服务器。
2. 三台电脑此时可同时连接同一台服务器进行游戏。（一台电脑既是服务器，又是客户端。）

复杂一些比如，三国战纪四人联机：
1. 四人同时连接服务器，进入游戏后。1P（选择游戏的人是1P）开启业务模式（Tab键-打开业务开关）
2. 按F3重装加载游戏，马上按住1P的除方向键的第一个键（比如我常用J作为我的第一个按键，一般游戏J表示轻拳）
3. 进入PGM设置，调整游戏为4人游戏。（记得是第三或者第四个设置的二级菜单里有，进去后慢慢试）
4. 关闭业务打开，按退出，重新启动游戏（按F3）。注意不是退出重连。

## 作弊器

需要下载作弊文件cheat.dat,放到模拟器根目录，并在选项-杂项中启用游戏作弊功能

## 出招表

一般模拟器都会自带游戏出招表，在游戏过程中按住**TAB**调出菜单，mame32 more这款模拟器的出招表在  游戏文档-显示指令列表。而mameplus则是在第一级菜单就有。

## 存档和读档

在游戏进行到任何情况下，都可以存档和读档，对于一些游戏时间长的游戏很有用。按住**TAB**调出菜单，在一般选项里可以设置存档和读档的快捷键。默认是按住shift+F7然后输入一个数学或者字母存档，单按F7然后输入指定数字字母的读档。