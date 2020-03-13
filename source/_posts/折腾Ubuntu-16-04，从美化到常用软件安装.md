---
title: 折腾Ubuntu 16.04，从美化到常用软件安装
tags:
  - Linux
  - 桌面系统
abbrlink: 2bf895cd
date: 2018-09-06 23:19:01
updated: 2018-09-07 18:44:01
---
## 更新历史

2018-9-7：

 - 完善文章细节：常用软件安装方法
 - 增加Ubuntu自定义设置

2018-9-6：分享Ubuntu 16.04的美化以及安装常用软件

## 前言

根据2018年2月桌面操作系统市场占比(下图)，Linux虽拥有众多桌面版本分支，如Ubuntu，Deepin，Kubuntu等，却仅仅占桌面操作系统全球市场份额的1.46%。

这其中原因有很多，对于个人的选择来说，影响最大是两个因素，一是使用界面，二是软件数量和质量。

这篇文章针对我个人的使用情况，解决从美化到软件安装的各种需求。

![](/pic/d22ff2eegy1fv0938f05lj20jg0ew42o.jpg)

......
<!-- more --> 

## 系统美化

### 安装主题：Arc GTK

```bash
sudo sh -c "echo 'deb http://download.opensuse.org/repositories/home:/Horst3180/xUbuntu_16.04/ /' >> /etc/apt/sources.list.d/arc-theme.list"
wget http://download.opensuse.org/repositories/home:Horst3180/xUbuntu_16.04/Release.key
sudo apt-key add - < Release.key
sudo apt update
sudo apt install arc-theme
```

### 安装图标：papirus-icon-theme-gtk

```bash
sudo add-apt-repository ppa:varlesh-l/papirus-pack
sudo apt update
sudo apt install papirus-gtk-icon-theme
```

### 应用主题图标：Unity-Tweak-Tool

```bash
sudo apt update
sudo apt install Unity-Tweak-Tool
```

## 常用软件安装

不喜欢Ubuntu Gnome桌面，比较喜欢Unity桌面，对于我当前使用的软件来说兼容性相当好。

### 运行Windows软件：[deepin-wine-ubuntu](https://github.com/wszqkzqk/deepin-wine-ubuntu)

```
cd ~
git clone https://gitee.com/wszqkzqk/deepin-wine-for-ubuntu.git deepin-wine-ubuntu
cd deepin-wine-ubuntu
chmod +x ./install
./install.sh
```

可解决下列日常软件安装需求：

- QQ

- 微信
- 百度网盘
- WinRAR
- 迅雷极速版
- 阿里旺旺

### 全局搜索：Albert

```bash
sudo add-apt-repository ppa:nilarimogard/webupd8
sudo apt update
sudo apt install albert
```



### 网络工具：[electron-ssr](https://github.com/erguotou520/electron-ssr/releases)

### 音乐播放器：[网易云音乐](https://music.163.com/#/download)

### 浏览器：[Chrome](https://www.google.com/intl/zh-CN_ALL/chrome/)

### 输入法：Fictx(可安装五笔输入法)

系统自带，安装五笔输入法方式如下：

```bash
sudo apt install fcitx-table-wubi
```



### Markdown写作：[Typora](https://typora.io/#download)

### 代码编辑：[Sublime Text 3](https://www.sublimetext.com/3)

### 下载工具：uGET

```bash
sudo apt install uget
```



### 剪贴板增强：copyq

```bash
sudo add-apt-repository ppa:hluk/copyq
sudo apt-get update
sudo apt install copyq
```



### 邮件，日历，联系人，任务：Thunderbird

```bash
sudo apt install thunderbird
```



### 截图工具：Shutter

```bash
sudo apt install thunderbird
```



### 虚拟机：VMware Workstation

```
# 下载最新版VMware Workstation：
wget https://www.vmware.com/go/getworkstation-linux
# 增加可以执行权限并执行
chmod +x getworkstation-linux
sudo ./getworkstation-linux
# 之后进入图形安装界面
```

#### 安装过程报错：无法在模块路径中找到主题引擎：“murrine”，[解决方法](https://blog.csdn.net/yzf0011/article/details/75215609?locationNum=10&fps=1)

### 系统备份还原：TimeShift

```bash
sudo apt-add-repository -y ppa:teejee2008/ppa
sudo apt update
sudo apt install timeshift
```



### 硬盘分区工具：Gparted

```bash
sudo apt-get install gparted
```



### 文件/文件夹比较工具：meld

```bash
sudo apt-get install meld
```



### 办公软件：[WPS Office](http://wps-community.org/downloads)

### 状态栏显示天气：[优客天气](http://www.ubuntukylin.com/application/show.php?lang=cn&id=270)

### 启动项管理：gnome-session-properties（系统自带）

### 状态栏显示网速：indicator-netspeed-unity

```bash
sudo apt-add-repository ppa:fixnix/netspeed
sudo apt-get update
sudo apt-get install indicator-netspeed-unity
# 启动
indicator-netspeed-unity &
```

### 阻止系统休眠：Caffeine

```bash
sudo add-apt-repository ppa:caffeine-developers/ppa
sudo apt-get update
sudo apt-get install caffeine
```

## 系统自定义设置

### 取消输入sudo需要密码

```bash
sudo gedit /etc/sudoers
# 只要在%sudo ALL=(ALL:ALL) ALL下面添加一行
username  ALL=(ALL) NOPASSWD: ALL
```

### tty终端显示中文

```bash
# 首先安装fbterm
sudo apt-get install fbterm

sudo gpasswd -a YOUR_USERNAME video
sudo setcap 'cap_sys_tty_config+ep' /usr/bin/fbterm
# 修改.profile，并添加以下内容
vi ~/.profile
# 如果在tty下就执行fbtrem
if [ "$TERM" = "linux" ]; then
  # exec fbterm
  LC_CTYPE=zh_CN.UTF-8 exec fbterm
fi
```

