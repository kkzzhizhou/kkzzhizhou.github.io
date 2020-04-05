---
title: GCP申请免费一年服务并无限续用
tags:
  - VPS
abbrlink: gcp-free-trial
date: 2017-10-25 00:00:00
updated: 2020-3-16 14:34:21
---

## 简介
2017年3月9日，Google Cloud试用由2个月变1年了。绑卡送300美刀，1年内使用。用最低配置来爬墙，每个月大约86GB流量，适用个人使用。
截止2019年9月23日，本人仍然在免费试用中，当然之后这个bug可能修复。

## 注意
国内银联信用卡/全球付无法注册。
亲测 VISA 和 腾讯运通卡 可以激活。
没有VISA卡 ? ！可以去淘宝看看，或者去银行办理。
学生可以办没有额度的VISA卡。
<!-- more --> 
## 申请
第一步：https://cloud.google.com ，地区选中国，亲测可行。

![gcp-free-trial-1.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-1.png)

第二步：填写个人信息

![gcp-free-trial-2.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-2.png)

申请成功后，会扣1美元，过一会儿会将1美元返回到信用卡。

## 配置
### 配置防火墙
由于默认的防火墙限制太多，我们需要修改防火墙规则。

直接访问 ： https://console.cloud.google.com/networking/firewalls/list

或者在菜单中依次点击 【网络】–>  【防火墙规则】 –> 【创建防火墙规则】

![gcp-free-trial-3.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-3.png)

### 申请静态IP
直接访问 ： https://console.cloud.google.com/networking/addresses/list
或者在菜单中依次点击 【网络】–>  【外部IP地址】 –> 【保留静态IP】
区域可选亚洲东部、欧洲、美国 等地。推荐亚洲！

![gcp-free-trial-4.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-4.png)

## 创建计算引擎
直接访问 ： https://console.cloud.google.com/compute/instances
或者在菜单中依次点击 【计算引擎】–>  【创建实例】

![gcp-free-trial-5.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-5.png)

注意以下配置，配置静态IP。

![gcp-free-trial-6.png](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-6.png)

### 配置SSH
1. 点击进入“元数据”

![gcp-free-trial-7.gif](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-7.gif)

2. 添加SSH密钥

![gcp-free-trial-8.gif](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-8.gif)

3. 启动你的软件PuttyGen，用软件生成一个Key,生成KEY的过程要不断地移动你的鼠标。[PuttyGen下载](https://www.freehao123.com/dl-puttygen/)

![gcp-free-trial-9.gif](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-9.gif)


4. 生成了Key后，先点击右下方的“保存私钥”，将密钥保存在本地。

![gcp-free-trial-10.gif](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-10.gif)

5. 然后复制上面的公钥到元数据中，注意在公钥最后加上你的用户名，然后点击保存。（点击放大）

![gcp-free-trial-11.gif](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-11.gif)

6. 现在打开Putty，填入IP地址与端口,**在授权中添加刚刚保存的私钥**。

![gcp-free-trial-12.gif](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-12.gif)

7. 如果你想使用Xshell，你需要在PuttyGen中导出为另一种Key格式（OpenSSH key）

![gcp-free-trial-13.gif](https://raw.githubusercontent.com/kkzzhizhou/kkzzhizhou.github.io/images/gcp-free-trial-13.gif)