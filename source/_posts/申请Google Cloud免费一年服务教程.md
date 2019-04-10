---
title: 申请Google Cloud免费一年服务教程
tags:
  - VPS
  - 福利
abbrlink: b2938d56
date: 2017-10-25 00:00:00
updated: 2017-10-25 00:00:00
---
## 简介
2017年3月9日，Google Cloud试用由2个月变1年了。绑卡送300美刀，1年内使用。用最低配置来爬墙，每个月大约86GB流量，适用个人使用。

## 注意
国内银联信用卡/全球付无法注册。
亲测 VISA 和 腾讯运通卡 可以激活。
没有VISA卡 ? ！可以去淘宝看看，或者去银行办理。
学生可以办没有额度的VISA卡。
<!-- more --> 
## 申请
第一步：https://cloud.google.com ，地区选中国，亲测可行。

![a][1]
第二步：填写个人信息

![b][2]

申请成功后，会扣1美元，过一会儿会将1美元返回到信用卡。

## 配置
### 配置防火墙
由于默认的防火墙限制太多，我们需要修改防火墙规则。

直接访问 ： https://console.cloud.google.com/networking/firewalls/list

或者在菜单中依次点击 【网络】–>  【防火墙规则】 –> 【创建防火墙规则】

![firewall][3]

### 申请静态IP
直接访问 ： https://console.cloud.google.com/networking/addresses/list
或者在菜单中依次点击 【网络】–>  【外部IP地址】 –> 【保留静态IP】
区域可选亚洲东部、欧洲、美国 等地。推荐亚洲！

![ip][4]
## 创建计算引擎
直接访问 ： https://console.cloud.google.com/compute/instances
或者在菜单中依次点击 【计算引擎】–>  【创建实例】

![vm][5]
注意以下配置，配置静态IP。

![network][6]
### 配置SSH
1. 点击进入“元数据”

![ssh1][7]
2. 添加SSH密钥

![ssh2][8]
3. 启动你的软件PuttyGen，用软件生成一个Key,生成KEY的过程要不断地移动你的鼠标。[PuttyGen下载][9]

![puttygen][10]
4. 生成了Key后，先点击右下方的“保存私钥”，将密钥保存在本地。

![key][11]
5. 然后复制上面的公钥到元数据中，注意在公钥最后加上你的用户名，然后点击保存。（点击放大）

![key-ssh][12]
6. 现在打开Putty，填入IP地址与端口,**在授权中添加刚刚保存的私钥**。

![putty][13]
7. 如果你想使用Xshell，你需要在PuttyGen中导出为另一种Key格式（OpenSSH key）

![openssh key][14]

### 搭建云免流SSR，一键安装BBR加速，Gost(UDP转TCP)，LNMP，

``` stylus
# 一键安装云免流SSR和Gost，适用于中国联通
wget http://cdn.yunmaopt.cc/jiaoben.sh && bash jiaoben.sh
# 一键安装最新内核并开启 BBR 脚本
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x ./bbr.sh&&bash bbr.sh
./bbr.sh
# 一键安装LNMP，如果无法使用screen命令，请使用yum install screen
screen -S lnmp
wget -c http://soft.vpser.net/lnmp/lnmp1.4.tar.gz && tar zxf lnmp1.4.tar.gz && cd lnmp1.4 && ./install.sh lnmp
```


[1]: https://lh3.googleusercontent.com/-aFMjAAC5xVA/WjZ2o7bhCDI/AAAAAAAAc9g/AE6wYV3nEHQYpIRAJKVTvbaBpYiIpUgAwCHMYCw/s0/2017-12-17_21-52-21.png
[2]: https://lh3.googleusercontent.com/-JX3UnQBJ4_Y/WjZ2nx4TUWI/AAAAAAAAc9c/U9-SvFoXQt0pkbJZqZSWbFts73AYOBxAwCHMYCw/s0/2017-12-17_21-52-21.png
[3]: https://lh3.googleusercontent.com/-Oe2G4U4GVR0/WjZ2lNQfTQI/AAAAAAAAc9E/48_ApRwT4McYAkTTSFfX3sQHju_UUepKgCHMYCw/s0/2017-12-17_21-52-21.png
[4]: https://lh3.googleusercontent.com/-CKXUwCYcUzA/WjZ2mT2EWVI/AAAAAAAAc9Q/vVlSCvnfCwUNT_uWZRzsMIpnAViUtohOgCHMYCw/s0/2017-12-17_21-52-21.png
[5]: https://lh3.googleusercontent.com/-VbjeSKmEWAg/WjZ2lAFwlMI/AAAAAAAAc9A/mDqIMllxOXwp3zTwAieg4JKlV9gbwhx7wCHMYCw/s0/2017-12-17_21-52-21.png
[6]: https://lh3.googleusercontent.com/-YNyFHjmJtqo/WjZ2l9s8GMI/AAAAAAAAc9M/daXEXFTHEGw_nfpYRw-SdSDlgszMrHTcwCHMYCw/s0/2017-12-17_21-52-21.png
[7]: https://lh3.googleusercontent.com/-mbbCI8A-U2g/WjZ2l7W9dmI/AAAAAAAAc9I/AYwpemTUhJsZqrnmiokXC2h5BlgMPdNBwCHMYCw/s0/2017-12-17_21-52-21.png
[8]: https://lh3.googleusercontent.com/-Ys5xrYw7HJk/WjZ2lD99LfI/AAAAAAAAc88/5Cn1k-OM4rsp6eOm3xUZeUGgtKRPDC0GACHMYCw/s0/2017-12-17_21-52-21.png
[9]: https://www.freehao123.com/dl-puttygen/
[10]: https://lh3.googleusercontent.com/-JJG1Rzd0zr0/WjZ2nRYYzfI/AAAAAAAAc9Y/UehvaCBDwcEXRr7Z6YJ0buBU5twzpy6fgCHMYCw/s0/2017-12-17_21-52-21.png
[11]: https://lh3.googleusercontent.com/-ZdfiFMf4MVg/WjZ2m_2E61I/AAAAAAAAc9U/2FfNk5glwHUhRkfoHHbQzqwnyGQlLIXxQCHMYCw/s0/2017-12-17_21-52-21.png
[12]: https://lh3.googleusercontent.com/-fg9vWhGti0A/WjZ2k_lRElI/AAAAAAAAc80/srQ06-KeFtAJmocq4zsPLtnXgX_1yT5bwCHMYCw/s0/2017-12-17_21-52-21.png
[13]: https://lh3.googleusercontent.com/-Z1UeNnq-v9s/WjZ2oSD8sqI/AAAAAAAAc9k/xEC3dNm9EbU7wRJZNc1M4zK1RZcbXZPpQCHMYCw/s0/2017-12-17_21-52-21.png
[14]: https://lh3.googleusercontent.com/-PUVbkxdxJHA/WjZ2kxJRC6I/AAAAAAAAc84/SmGdweSQunsp0F09x_JKYnyDCOvBQQgyACHMYCw/s0/2017-12-17_21-52-21.png