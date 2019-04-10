---
title: Windows同步阅读Kindle个人文档的可行方案
tags:
  - Kinlde个人文档
  - Windows
  - AHK应用
abbrlink: d9a27f8c
date: 2018-08-31 14:49:35
updated: 2018-08-31 14:49:41
---

## 更新历史

- 2018-8-31：第一个版本

## 前言

众所周知，Kindle支持在安卓和IOS设备中同步阅读个人文档，但Kindle for PC并不支持。

### 网上找到的解决方案如下：

1. 将书籍放到My Kindle Content中阅读
2. Chrome ARC Welder安装Kindle
3. 使用安卓模拟器

### 首先分析以上三种方案

方案一：可以打开并阅读书籍，但书签，笔记，阅读进度不能同步。（不可行）

方案二：可以打开并登录Kindle，非常卡顿，而且在阅读界面会崩溃。（不可行）

方案三：虚拟一个安卓系统，但存在一些阅读便捷性问题，我的方案主要解决的是一些阅读便捷性问题。（可行）

<!-- more --> 

## 我的方案

准备工具：

1. [Nox 夜神模拟器海外版](https://en.bignox.com/)，我使用的版本是6.0.5.2，这版本默认是绿色便携版，可放在U盘中使用。
2. [AutoHotKey](https://autohotkey.com/)，使用官方最新版

解决的问题：

1. Kindle阅读时使用鼠标滚动翻页
2. 使用鼠标中键单击返回
3. 使用鼠标中键双击最近任务
4. 使用鼠标中键长按后释放返回主页
5. 两种鼠标中键滚轮模式切换：阅读模式和常规模式

```
;=====================================================================
;           按住右键+鼠标滚轮往上:音量加                             
;                    鼠标滚轮往上:向上滚动                           
;           按住右键+鼠标滚轮往下:音量减                             
;                    鼠标滚轮往下:向下滚动                           
;                    鼠标中键单击:返回键                             
;                    鼠标中键双击:最近任务                           
;                    鼠标中键长按:主页键                             
;           按住右键+鼠标中键长按:模式切换(阅读模式和常规模式)       
;           按住右键+鼠标中键长按:Nox全屏
;           阅读模式:在Nox中,鼠标滚轮代表音量加减,用于翻页                
;           常规模式:鼠标滚轮为正常上下滚动   
;                      zzz-2018.08.31                                
;---------------------------------------------------------------------                                                                                  
#IfWinActive ahk_exe Nox.exe                                         
{                                                                    
Flag:=false                                                          
MButton::                                                            
if pressesCount > 0 ; ＞0说明SetTimer 已经启动了，按键次数递增       
{                                                                    
    pressesCount += 1                                                
    return                                                           
}                                                                    
;否则，这是新一系列按键的首次按键。将计数设重置为 1 ，并启动定时器： 
pressesCount = 1                                                     
SetTimer, WaitKey, 500 ;在 500 毫秒内等待更多的按键。                
return                                                               
                                                                     
WaitKey:                                                             
KeyWait, MButton                                                     
If (A_TimeSinceThisHotkey > 500)                                     
	{                                                                
	send,{Home}                                                      
	SetTimer, WaitKey, off                                           
	pressesCount = 0                                                 
	return                                                           
	}                                                                
SetTimer, WaitKey, off                                               
if pressesCount = 1 ;该键已按过一次。                                
{                                                                    
    Gosub singleClick                                                
}                                                                    
else if pressesCount = 2 ;该键已按过两次。                           
{                                                                    
	Gosub doubleClick                                                
}                                                                     
;不论上面哪个动作被触发，将计数复位以备下一系列的按键：              
pressesCount = 0                                                     
return                                                               
                                                                     
singleClick:                                                         
if GetKeyState("RButton") = 0                                        
	Send, {ESC}                                                      
else                                                                 
{                                                                    
	if(Flag:=!Flag)                                                  
	{                                                                
		wheelup::                                                    
		if GetKeyState("RButton") = Flag                             
			Send, {wheelup}                                          
		else                                                         
			send, ^6                                                 
		return                                                       
		wheeldown::                                                  
		if GetKeyState("RButton") = Flag                             
			Send, {wheeldown}                                        
		else                                                         
			send, ^7                                                 
		return                                                       
	}                                                                
}                                                                    
return                                                               
                                                                     
doubleClick:                                                         
if GetKeyState("RButton") = 0                                        
	Send, {End}                                                      
else                                                                 
	send, ^5                                                         
return                                                               
                                                                     
}                                                                    
;---------------------------------------------------------------------
```

