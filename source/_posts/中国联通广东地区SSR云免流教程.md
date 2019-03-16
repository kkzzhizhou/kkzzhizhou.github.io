---
title: 中国联通广东地区SSR云免流教程
date:  2017-10-9
updated: 2018-4-5
tags: [云免流,SSR]
---

## 更新日志 ##

- 2018-4-5： 使用参数**short.weixin.qq.com**使用的是微信定向流量
- 2018-3-30：免流参数**ylsh.gd10010.cn**失效
- 2018-2-20：更新注意事项,配置参数,ssrscriptn使用方法
- 2018-1-11：免流参数**ylsh.gd10010.cn**可用
- 2017-11-7：免流参数**aop.gd10010.cn**失效

## 免流原理
运营商为了给客户提供方便，提供了一些优惠政策，如：接收彩信、登陆掌厅免除流量费以及免收取流量费的其他业务。 
运营商的计费系统为了区分用户使用的是免流量业务还是正常访问互联网会把这些免流服务的网址加入到白名单，这些白名单中的网址就是我们平常所说的免流IP了，当计费系统检测到用户访问的是白名单中的网址或接收彩信时就不会进行扣费。 

## 注意事项 ##

- **如果服务器长时间高速免流下载，联通会采取封IP的措施，切记**
- **此次分享是中国联通免流的教程，中国移动，中国电信不可用**

<!-- more --> 

## 免流教程
1. 首先，你得有一台VPS，~~带宽建议大于100M~~，如果需要免流顺带科学上网，可以考虑购买国外的VPS。
2. 用SSH软件（如xshell,putty等）登录VPS。执行一键安装脚本
``` stylus
wget http://cdn.yunmaopt.cc/jiaoben.sh && bash jiaoben.sh
```
3. 在提示界面中安装**SSR一键安装**，端口选择**443**
4. 在提示界面中安装 **Gost一键安装**，密码和端口自定义。
5. 手机端使用SSR时，正常配置SSR连接，还需要在混淆插件（OSBF为http_simple）下配置混淆参数为~~aop.gd10010.cn~~  **ylsh.gd10010.cn**，配置SSR为**全局模式以及UDP转发**。
``` lsl
SSR+关键配置如下（其余参数默认即可）：
服务器：填写服务器IP地址
远程端口：443
密码：SSR密码
加密方式：chacha20
协议：auth_sha1_v4
混淆方式：http_simple
混淆参数：ylsh.gd10010.cn
UDP代理方式：通过TCP转发
UDP代理规则：全局代理
```

## 共享SSR网络（需Root）
在使用官方的SSR免流时，启用手机热点，其他设备是无法正常上网的。
需要使用**ssrscriptn**这款软件来进行SSR连接。
![ssr+](https://lh3.googleusercontent.com/-MleBy9zkIhw/WowHTKvTcGI/AAAAAAAAdfA/wWVGarjsxnkCo0YtRi-7Rl_KpsOPX8dAQCHMYCw/s0/2018-02-20_19-32-25.png)




