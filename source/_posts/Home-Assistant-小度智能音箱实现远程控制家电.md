---
title: Home Assistant+小度智能音箱实现远程控制家电
comments: true
date: 2020-03-16 17:47:25
updated: 2020-03-16 17:47:25
tags: 
- 米家WIFI智能插座
- 智能家居开源系统
- 群晖DSM
categories: 
- [智能家居]
abbrlink: home-assistent-with-xiaodu-smart-speaker
---

## 引言

在联通营业厅更换宽带套餐时加钱买了个小度智能音箱，从一开始只是查查天气、放放歌，我现在它做得更多一些，比如说本篇教程提到的控制家里的电器。

<!-- more --> 

## 准备

- 群晖DSM使用Docker下载安装homeassistant/home-assistant
- 购买小米米家智能插座插头WiFi版

## Home Assistant配置步骤

![Docker使用1](/pic/home-assistent-with-xiaodu-smart-speaker-1.png)

![Docker使用2](/pic/home-assistent-with-xiaodu-smart-speaker-2.png)

![Docker使用3](/pic/home-assistent-with-xiaodu-smart-speaker-3.png)

![Docker使用4](/pic/home-assistent-with-xiaodu-smart-speaker-4.png)

![Docker使用5](/pic/home-assistent-with-xiaodu-smart-speaker-5.png)

应用后启动即可,配置界面连接为http://nas_ip:8123

## 扩展：公网Https方式访问Haome Aassistant

如果需要在公网中使用Home Assistant,可以使用内网穿透工具frp。Home Assistant默认监听本地8123端口,使用Websocket连接。

### nginx配置

```
server {
    listen 443 ssl;
    server_name hass.domain.com; # 修改domain为你自定义的域名
    ssl_certificate       /etc/nginx/ssl/domain.com.key.pem; # 修改domain为你自定义的域名
    ssl_certificate_key   /etc/nginx/ssl/domain.com.key; # 修改domain为你自定义的域名
    ssl_session_timeout 5m;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    location / {
        proxy_set_header Host  $http_host;
        proxy_pass http://127.0.0.1:[frp_port]; # 此处修改为你的frps端口
    }
    location /api/websocket {
        proxy_pass http://127.0.0.1:8123;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

### frpc配置

```
[hass-ws]
type = tcp
local_ip = 127.0.0.1
local_port = 8123
remote_port = 8123

[hass]
type = http
local_ip = 127.0.0.1
local_port = 8123
custom_domains = hass.domain.com
```

## 参考文章

- [哑虎的智能家居路 篇四：小度音箱接入HomeAssistant](https://post.smzdm.com/p/amm0g5qd/)

## 智能家居论坛

- https://bbs.hassbian.com/forum.php