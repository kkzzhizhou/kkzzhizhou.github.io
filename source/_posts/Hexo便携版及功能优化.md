---
title: Hexo便携版及功能优化
tags:
  - Portable
categories:
  - Hexo
toc: false
date: 2018-07-07 10:21:16
---

Hexo作为一种静态博客，重新配置可以说是相当的繁琐，于是有了Hexo便携版（感谢@比特萌信息技术提供的HEXO Portable），现在官网已经打不开（截至2018-7-7），幸好我做了安装包备份。以下的教程将对Hexo Portable这个软件做进一步的优化处理。

## 整合多个批处理

原来的：

![origin](https://lh3.googleusercontent.com/-mi8ZUeN5ACc/W0AmN2HfPtI/AAAAAAAAeXE/7NJyeH4d0moG8RHSAgPxlUjyteYfliMlACHMYCw/s0/explorer_2018-07-07_10-32-14.jpg)

处理后：

![hexo_bat](https://lh3.googleusercontent.com/-31dt0w4QU78/W0AmvKhh9bI/AAAAAAAAeXM/Rpq4HpuiLTkvh2knyaWx7O8-E9IbYjfoQCHMYCw/s0/cmd_2018-07-07_10-34-36.jpg)

并在打开批处理时同时打开文章所在的文件夹：

`start %cd%\source\_posts `

......

<!-- more --> 

## 添加新功能

### 1. 将源文件备份到bitbucket私有仓库

`start git-bash "%cd%\..\support\script\Backup.sh"`

### 2. 从bitbucket恢复到本地

`start git-bash "%cd%\..\support\script\Restore.sh"`



### 源代码

``` 
@echo off & title Hexo(zzz脚本)
mode con cols=50 lines=25
color 2F
cd blog
::打开批处理同时打开文章所在的文件夹
start %cd%\source\_posts
echo 正在初始化...
set path=%path%;%cd%\..\support\git\bin\;%cd%\..\support\nodejs\;%cd%\..\blog\node_modules\.bin;%cd%\..\support\nodejs\node_modules\.bin;%cd%\..\support\git\
:Menu
cls
@ echo.
@ echo.    ==================目录====================
@ echo.     
@ echo.          1. 配置Github部署
@ echo.
@ echo.          2. 配置基本信息
@ echo.  
@ echo.          3. 启动命令行
@ echo.  
@ echo.          4. 创建新文章
@ echo.         
@ echo.          5. 生成并本地测试
@ echo.       
@ echo.          6. 生成并部署
@ echo.        
@ echo.          7. 重置配置文件
@ echo.     
@ echo.          8. 从bitbucket中恢复数据
@ echo.
@ echo.          9. 备份到bitbucket
@ echo.
@ echo.          10. 一键生成部署同步
@ echo.
@ echo.    ==========================================
@ echo.
set /p xj= 输入数字按回车：
if /i "%xj%"=="1" Goto Setup
if /i "%xj%"=="2" Goto Basic
if /i "%xj%"=="3" Goto Term
if /i "%xj%"=="4" Goto New
if /i "%xj%"=="5" Goto GenerateAndServer
if /i "%xj%"=="6" Goto GenerateAndDelpoy
if /i "%xj%"=="7" Goto Reset
if /i "%xj%"=="8" Goto Restore
if /i "%xj%"=="9" Goto Backup
if /i "%xj%"=="10" Goto Onekey
@ echo.
echo 　　　  选择无效...请重新输入...
ping -n 2 127.1>nul
goto menu
:Setup
start git-bash "%cd%\..\support\script\deploy.sh"
goto menu
:Basic
start git-bash "%cd%\..\support\script\configSet.sh"
goto menu
:Term
start git-bash "%cd%\..\support\script\start.sh"
goto menu
:New
start git-bash "%cd%\..\support\script\newPost.sh"
goto menu
:GenerateAndServer
start git-bash "%cd%\..\support\script\generateAndServer.sh"
goto menu
:GenerateAndDelpoy
start git-bash "%cd%\..\support\script\generateAndDelpoy.sh"
goto menu
:Reset
del %cd%\_config.yml
copy %cd%\..\support\backup\_config.yml _config.yml
:Restore
cd ..
rd /s /q blog
md blog
cd blog
start git-bash "%cd%\..\support\script\Restore.sh"
goto menu
:Backup
start git-bash "%cd%\..\support\script\backup.sh"
goto menu
:Onekey
start git-bash "%cd%\..\support\script\onekey.sh"
cls
goto menu
```