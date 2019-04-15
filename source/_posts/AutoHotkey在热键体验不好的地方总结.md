---
title：AutoHotkey在热键体验不好的地方总结
date: 2019-4-14 14:2:39
updated: 2019-4-14 14:2:43
author: zzz
tags: AHK,Hotkey
categories: 效率提升

---

## 最开始的想法

- 长按字母键打开常用应用，不影响字母输入
- 长按鼠标中键打开指定应用，不影响鼠标中键原有功能
- 双击Alt唤醒Wox，不影响Alt原有功能

## 失败后的备选方案

- 使用RShift + 字母打开常用应用
- 使用Wgesture，定义按下鼠标右键+单击鼠标左键打开指定应用（已实现）
- 使用Capslock + F发送Alt+Space，实现唤醒Wox（已实现）

## 意外收获

发现火萤酱快捷键能够设置双击Alt来唤醒，这就说明用其他语言能够完美的实现双击热键。

## 无效例子1：长按字母键影响输入

来源：[仅长按单键执行功能，不影响短按示例](https://www.autohotkey.com/boards/viewtopic.php?f=28&t=6082)

```
;示例代码
$t::
	KeyWait, t
	If (A_TimeSinceThisHotkey > 300)
		SetTimer, mainp, -1
	Else
		SendInput, % GetKeyState("CapsLock", "T") ? "T" : "t"
Return

mainp:
	Run, http://www.baidu.com
Return
```

从功能上我们是希望达到以下效果：

- 当单击时，输入小写字母t，如果有大写锁定，则输入大写字母T
- 当长按时，执行打开百度的操作

但实际这有许多体验很差的地方，比如：

- 当我打字比较快的时候，输入tf，结果输入的是ft，是因为t需要等待时间处理才会输出。

## 在对以上代码改造后

```ahk
;在对以上代码改造后
$MButton::
	KeyWait, MButton
	If (A_TimeSinceThisHotkey > 300)
		SetTimer, mainp, -1
	Else
		Click, M
Return

mainp:
	Send, {F3}
Return
```

这代码不能正常工作，我希望长按中键时打开指定应用，单击时执行中键原来的功能，结果是长按鼠标中键能打开指定应用，但无法正常使用鼠标中键

## 无效例子2：按键双击检测

 来源:[热键的次数与时长- AutoHotkey Community](https://autohotkey.com/boards/viewtopic.php?t=4286)

```
;修改原来的RControl为LAlt
intInterval := 500 ; 若两次连击在这个时间间隔中，则视为双击。
~LAlt::
if (A_PriorHotkey <> "~LAlt" or A_TimeSincePriorHotkey > intInterval)
{
    KeyWait, LAlt
    return
}
MsgBox, 您双击了左边的 LAlt 键。
return
```

功能是希望双击左边的Alt执行打开，但问题是在编辑器长按Alt多选会出现鬼畜现象，影响Alt多行编辑的使用。

```
;修改原来的#c为LAlt
LAlt::
if (intCount > 0) ; SetTimer 已经启动，这里记录键击。
{
    intCount += 1
    return
}

intCount = 1
SetTimer, KeyWinC, 400 ; 在 400 毫秒内等待更多的键击。
return

KeyWinC:
SetTimer, KeyWinC, off
if (intCount = 1) ; 此键按下了一次。
{
    Run, m:\
}
else if (intCount = 2) ; 此键按下了两次。
{
    Run, m:\multimedia
}
else if (intCount > 2)
{
    MsgBox, 连击了三次或更多。
}
intCount = 0
return
```

运行后会使用原来的Alt功能失效，比如Alt+Tab无法使用。

