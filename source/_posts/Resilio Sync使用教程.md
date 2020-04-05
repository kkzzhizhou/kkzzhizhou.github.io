---
title: Resilio Sync使用教程
date: 2017-4-13
updated: 2017-4-13
tags: Resilio Sync
abbrlink: resilio-sync-tutorial
---

## 问题

无法获取追踪器列表，没有可用的跟踪程序连接，无法链接设备

<!-- more -->

## 解决方法

科学上网-大陆白名单

## Resilio Sync 使用教程

1. 下载安装包：https://download-cdn.resilio.com/stable/windows64/Resilio-Sync_x64.exe
2. 如下图所示，按下一步

![resilio-sync-tutorial-1.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/resilio-sync-tutorial-1.png)

3. 安装成功后，如下图所示

![resilio-sync-tutorial-2.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/resilio-sync-tutorial-2.png)

4. 添加密钥

![resilio-sync-tutorial-3.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/resilio-sync-tutorial-3.png)

![resilio-sync-tutorial-4.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/resilio-sync-tutorial-4.png)

**PS:选择性同步仅同步你想要同步的文件，关闭的情况下同步所有的文件**
1. 选择保存路径，文件就可以自己同步。

## 无限试用方法

1. 安装 Resilio Sync （废话）
2. 点击“试用 Pro 版 30 天”
3. 打开程序的安装目录，找到License文件夹，用编辑器打开 license.bin ，你会看到一些乱码，没关系，把 expirationixxxxxxxxxxxx （你的许可到期时间）改成 expirationi1766477045e5 ，1766477045e5的意思是 2025/12/23 16:04:05，所以这相当于无限试用了吧2333

## 2017-6-11：Resilio Sync 无法获取追踪器列表的解决办法
今天碰到这样的问题--软件件下方提示 无法获取追踪器列表 的，英文版本提示 cannot get the list of trackers
目前解决的办法也很简单。
**WINDOWS 用户修改 C:\Windows\System32\drivers\etc\hosts
Linux Mac 等用户修改 /etc/hosts**
用记事本打开修改就可以
添加下面一行
**54.230.143.112   config.getsync.com**
修改后如下
退出重新启动 Resilio Sync 软件。就可以飞起来了，少年加油.

**PS: 此后使用过程中一直会显示“Sync Pro | 还剩 30 天”的字样**

##  自己收藏的资源密钥
### 电子书库
编程随想：
BRSSYZTSAC6UGYTUOJ22L4GCO7QESPPBD    政治
BNZ6DOA6W577O6GUNH7C3MY6DWC6FTDQB    心理学
BSH7FXJFVWJTKWGSX5GTWX7PHZZ2D2M7Q    历史
B2FRYA6AXCDW6CF4YJVFWKH2HAXOFICOX    经济
B3WNBTAAFFAODFR6FQ3E3L5BBSJAFNBSJ    管理
BZR4TTYHT25QWUIE6YNMAKWUGBHKSGLC6    社会学
BMBB5YLBIJJAE5H6TP27OS7YCEUKCYHZK    文艺
B6WWVBXPMZDI5IL4KED6AAHA5FO4UNKQF    哲学
BMWWZALG4P56LREF47EE2WSWHZEM4E6BL    军事
BUPSDXFA3TP7KCMLHALRHLIX2FEJEUJFE    IT
mebook.cc
BN5T34NFGECAYDRF4DW2QFCJZQN4IZ4O7    2016年以前
BLPBKUS7BUVOEQP7NLLPBATBQ5RYXFVXR    最近更新
kindlefere.com
BOC3NIGPF2DOKETOF2FAHXJXE2HF24QWC    中文
BZGL26OZ4AFMOYFXJ4WGI4YIG4LOIDA43	 英文
B4TDKK7OLYBW7OAG3ILYLQPLFK3QSTAS4	 每周一书
BLE2YCVCA3JPQCRZGDQVTFTKQYPDH5MQC	 kindle伴侣系列推荐
BBADTVEZKA34CG7XCW4AWTBG6FWFDWAGC    经济学人2013-2016
电子书库
BQ36ZETYSW4SLJ2VMPIGXATAEMXYKXDHT    丛书系列
BZCTXN7QYCMXS5PINIEO3JU7C7YFI6GOR    主题分类
B7ZJOFU5YGHTVQOT42JLGOULNTPTZ73FS    科普读物 
BR5XUQVQL7QFJBIIKFSAETAFCPANTBRCO    学习书单 
BZ7VZSMPAORFQ2FP5PSJK4P2PAND6WD66    网友荐书
### 站点分享
#### 2017-6-11更新
- **微力同步 Resilio Sync Key： http://verysync.com/**
#### 之前分享

 - btsync吧：http://tieba.baidu.com/f?kw=btsync&ie=utf-8 
 - Resilio Sync Keys List：http://changlai.net/
 - 知乎问答：https://www.zhihu.com/question/21517918
 - BT资源导航：http://wherebt.com/ btsync：http://btsync.space/
 - BTSync中文发布站：https://btsync.org/