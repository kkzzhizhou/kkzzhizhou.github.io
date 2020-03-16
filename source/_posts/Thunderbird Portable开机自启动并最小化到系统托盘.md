---
title: Thunderbird Portable开机自启动并最小化到系统托盘
tags:
  - Thunderbird Minimize
  - AHK应用
abbrlink: thunderbird-minimized-auto-start
date: 2018-08-31 15:28:36
updated: 2018-08-31 15:28:36
---

## 问题描述

1. 便携应用设置为开机启动时会自动打开主界面
2. Thunderbird 60.0官方并不支持最小化到系统托盘
3. Thunderbird 第三方最小化到系统托盘的插件如FireTray，最多支持到54.X，在最新版的Thunderbird中并不可用。

<!-- more --> 

## 可行解决方案：AHK，全称AutoHotkey

```
;=====================================================================
;                 Thunderbird Portable 60.0+ Tray
;                            Author:zzz
;                           date:2018-8-31
;             使用方法：将AHK放在ThunderbirdPortable.exe目录中运行
;               理论上支持所有Thunderbird版本，包括以后发布的版本
;---------------------------------------------------------------------

#NoEnv
SendMode Input  
SetWorkingDir %A_ScriptDir%  
DllCall("kernel32.dll\SetProcessShutdownParameters", UInt, 0x4FF, UInt, 0)
#SingleInstance ignore
menu,tray,icon,App\AppInfo\appicon.ico
;title must contain
SetTitleMatchMode, 2

Run, ThunderbirdPortable.exe
WinWait, ahk_exe Thunderbird.exe
;WinMinimize, ahk_exe Thunderbird.exe
WinHide, ahk_exe Thunderbird.exe


OnExit, ExitSub

OnMessage(0x404, "AHK_NOTIFYICON")
OnMessage(0x11, "WM_QUERYENDSESSION") 
AHK_NOTIFYICON(wParam, lParam)
{
    if (lParam = 0x202) ; WM_LBUTTONUP
	{
		WinShow, - Mozilla Thunderbird
		WinActivate, - Mozilla Thunderbird
	}
}
WM_QUERYENDSESSION(wParam, lParam)
{
  ENDSESSION_LOGOFF = 0x80000000
  Process,Close,Thunderbird.exe
  Process,WaitClose,ThunderbirdPortable.exe
}

ProcessExist(Name){
	Process,Exist,%Name%
	return Errorlevel
}

Loop
{
	If !ProcessExist("thunderbird.exe")
	{
		ExitApp
	}
	
	WinGet, winState, MinMax, ahk_exe thunderbird.exe
	if (winState = -1) {
		WinHide, - Mozilla Thunderbird
	}
   
	sleep 500
}

ExitSub:
WinClose,ahk_exe thunderbird.exe
Process,close,Thunderbird.exe
ExitApp
```

