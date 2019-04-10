---
title: GCP安装配置Hexo全过程
date: 2018-1-20
updated: 2018-2-20
tags:
  - VPS
  - Google Cloud Platform
  - 服务器
abbrlink: 2f07c9ad
---
## 原因
1. 从2016年建立个人博客开始使用Wordpress，了解Wordpress强大的同时，也认识到Wordpress的繁琐，最烦恼的是数据库文章的问题，比如说Wordpress文章ID不连续，在使用Google Cloud Platform后数据库时不时无法连接。
2. 相比于Wordpress,Hexo属于静态博客，所有源数据都放在本地，生成网站数据后发布到网上，虽然过程相对繁琐，但访问速度快，使用Github Pages后相当于无限流量。

<!-- more --> 

## 搭建Hexo博客
### 1. 登录Google Cloud Platform（即GCP）:[Compute Engine(链接)](https://console.cloud.google.com/compute/)

### 2. 创建实例

![创建实例-1](https://lh3.googleusercontent.com/-a2kyWhScN3A/WnVEhy1joAI/AAAAAAAAdVQ/p_PpNPaTgHQ0rQ7AJGvwuVuus_Ypvq7uACHMYCw/s0/chrome_2018-02-03_13-10-52.png)
![创建实例-2](https://lh3.googleusercontent.com/-qpZOKb-hbgs/WnVRI0Y5QYI/AAAAAAAAdWE/vkbLgkEe6ZAX1ELUObE1ZK1j_2jUMpJGACHMYCw/s0/chrome_2018-02-03_14-05-07.png)

拉到最下面确认创建新实例，创建后自动启动实例：

![实例创建成功](https://lh3.googleusercontent.com/--9_R0T4NiW0/WnVGbZ-7V9I/AAAAAAAAdVk/WMCOGu37ftUY2llV0qVTXrIyStBo1tl0wCHMYCw/s0/chrome_2018-02-03_13-19-25.png)

启用实例的SSH：

![登录VPS](https://lh3.googleusercontent.com/-EXobSRnOyRE/WnVHPZrSpSI/AAAAAAAAdVw/CNCATdG_ATYOjgN5ATL6mY_vEKkOYtKQACHMYCw/s0/chrome_2018-02-03_13-22-57.png)

![登录成功](https://lh3.googleusercontent.com/-rJH8zuJdLh8/WnVHhYqej3I/AAAAAAAAdV0/8sKFGDl2A5Ej4s8tgwprl2plTgwND0xtQCHMYCw/s0/chrome_2018-02-03_13-24-02.png)

1. 使用sudo passwd设置Root密码
```
sudo passwd //设置Root密码
```
2. 通过sudo su命令切换到root用户
``` stylus
sudo su //切换到root用户
```
3. 修改SSH配置文件/etc/ssh/sshd_config
``` stylus
vi /etc/ssh/sshd_config //编辑文件
```
4. 找到PermitRootLogin和PasswordAuthentication
``` stylus
LoginGraceTime 120
PermitRootLogin yes //默认为no，需要开启root用户访问改为yes
StrictModes yes
PasswordAuthentication yes //默认为no，改为yes开启密码登陆
```

5. 重启SSH服务使修改生效，Ubuntu同样适用
``` stylus
/etc/init.d/ssh restart
```

### 3. 查看当前Git版本
``` stylus
git --verison
```
### 4. 安装Node.js
``` stylus
sudo apt-get install nodejs -y
sudo apt-get install npm -y
```

### 5. 安装Hexo
``` stylus
npm install -g hexo-cli
```

#### 5.1 配置Hexo
``` stylus
# 进入想要存放博客的文件夹
hexo init
npm install
```
*报错：npm WARN optional Skipping failed optional dependency /chokidar/fsevents:
npm WARN notsup Not compatible with your operating system or architecture: fsevents@1.1.3
原因：fsevent是mac osx系统的，你是在win或者Linux下使用了 所以会有警告，忽略即可*
#### 5.2 安装主题
``` stylus
# 进入主题文件夹themes
git clone https://github.com/theme-next/hexo-theme-next
# 修改配置文件_config.yml，在theme字段中填入：hexo-theme-next即可
vi _config.yml
```
### 5.3 启动Hexo
``` stylus
hexo s
# 启动后在浏览器的地址栏填入：ip:4000即可启动
```
## 在Windows下写作
### 使用MarkdownPad 2 Pro
![](https://lh3.googleusercontent.com/-nenDps21_yE/Wovf1wKs8MI/AAAAAAAAdes/3OUK8YqxctYUAVwWKSqPAo303P7jVh9jgCHMYCw/s0/2018-02-20_16-44-04.png)
