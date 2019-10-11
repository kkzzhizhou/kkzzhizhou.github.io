---
title: CMD、Powershell、Bash终端配置走代理
date: 2019-4-19 10:12:6
updated: 2019-10-11
author: zzz
---

### CMD

```
;; 设置代理(其中sock5可以设置为http，https)
set http_proxy="sock5://127.0.0.1:1080"
set https_proxy="sock5://127.0.0.1:1080"
;; 清除代理设置
set http_proxy=
set https_proxy=
```

## Powershell

```powershell
# NOTE: registry keys for IE 8, may vary for other versions
$regPath = 'HKCU:\Software\Microsoft\Windows\CurrentVersion\Internet Settings'
# 清除代理设置
function Clear-Proxy
{
    Set-ItemProperty -Path $regPath -Name ProxyEnable -Value 0
    Set-ItemProperty -Path $regPath -Name ProxyServer -Value ''
    Set-ItemProperty -Path $regPath -Name ProxyOverride -Value ''

    [Environment]::SetEnvironmentVariable('http_proxy', $null, 'User')
    [Environment]::SetEnvironmentVariable('https_proxy', $null, 'User')
}
# 设置代理
function Set-Proxy
{
    $proxy = 'sock5://127.0.0.1:1080'

    Set-ItemProperty -Path $regPath -Name ProxyEnable -Value 1
    Set-ItemProperty -Path $regPath -Name ProxyServer -Value $proxy
    Set-ItemProperty -Path $regPath -Name ProxyOverride -Value '<local>'

    [Environment]::SetEnvironmentVariable('http_proxy', $proxy, 'User')
    [Environment]::SetEnvironmentVariable('https_proxy', $proxy, 'User')
}
```

## Bash

```bash
export ALL_PROXY="socks5://127.0.0.1:1080"
export http_proxy="http://127.0.0.1:1080"
export https_proxy="http://127.0.0.1:1080"
```

### 注意：

如果代理服务器需要登陆，这时可以直接把用户名和密码写进去

```bash
http_proxy=http://userName:password@proxyAddress:port
```

