---
title: 解决使用第三方输入法在LaunchPad中无法切换中英文
tags:
  - MacOS_Bug
  - Keyboard Maestro应用
abbrlink: 2d59f42c
date: 2018-09-02 00:20:30
updated: 2018-09-02 00:20:30
---

## 更新历史

- 2018年09月02日：利用Keyboard Maestro解决问题

## 问题描述

第三方输入法（如搜狗拼音输入法，清歌五笔输入法等）在Launchpad中无法使用Shift按键切换中英文输入，而是在Launchpad中显示烦人的输入框。

## 解决方法

1. 在Keyboard Maestro中新建一个Macros
2. 触发方式设置为Hot Key Trigger，条件为打开Launchpad的快捷键
3. 程序如下图所示

![程序截图](/pic/d22ff2eegy1fuujeecmvyj20ey0c3gn5.jpg)

本文到此结束。

<!-- more --> 