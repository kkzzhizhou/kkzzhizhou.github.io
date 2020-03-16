---
title: Scoop-Windows包管理器教程
tags: 包管理器
abbrlink: scoop-tutorial
date: 2020-12-16 12:00:00
updated: 2020-3-16 16:57:02
---

## 安装Scoop

[Scoop官网](https://scoop.sh/)

[Scoop-Github](https://github.com/lukesampson/scoop)

```
# 打开Powershell(非管理员)
Set-ExecutionPolicy RemoteSigned -scope CurrentUser


# 自定义Scoop安装目录
$env:SCOOP='D:\Scoop'
[Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')

# 安装Scoop命令
Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')

# 或者
iwr -useb get.scoop.sh | iex

```
## 使用Scoop安装卸载软件

```
scoop install 7zip git-with-openssh
scoop uninstall 7zip git-with-openssh
```

## 使用Scoop添加移除仓库

```
# 查看仓库列表
scoop bucket list
# 查看推荐仓库
scoop bucket known
# 添加推荐仓库
scoop bucket add extras
# 添加第三方仓库
scoop bucket add [bucket-name] [git-repo]
scoop bucket add zapps https://github.com/kkzzhizhou/scoop-zapps
# 移除仓库
scoop bucket rm [bucket-name]
scoop bucket rm extras
```

## 自建软件仓库

[官方教程](https://github.com/lukesampson/scoop/wiki)

## 合并多个软件仓库

[mergebucket.sh](../attachments/28090.sh)

## 软件仓库自动更新

[Excavator](https://github.com/ScoopInstaller/Excavator)

### 使用Docker自动更新

- 修改项目bin\auto-pr.ps1中是项目名称
- 新建docker-compose.yml文件，内容如下：
  
	```
	version: "3"
	
	services:
	  bucket:
	    image: r15ch13/excavator:latest
	    deploy:
	      mode: global # creates only one container
	    volumes:
	      - /usr/local/scoop/.ssh:/root/.ssh
	      - /usr/local/scoop/log:/root/log
	    environment:
	      GIT_USERNAME: "xxx"
	      GIT_EMAIL: "xxx@gmail.com"
	      BUCKET: "xxx/xxx"
	```

- 修改environment中的变量
- 修改volumes中.ssh映射目录，将私钥放入.ssh目录中
- 启动Docker

	```
	screen -S scoop
	docker-compose up
	```
