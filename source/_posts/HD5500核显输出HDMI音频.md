---
title: 黑苹果HD5500核显输出HDMI音频
date: 2018-3-30
updated: 2018-4-1
tags:
  - Hackintosh
  - HDMI Audio
abbrlink: 9053bcbc
---
## 驱动原理
1. 注入的ID可以是16160002或者是16260006
2. 在DSDT中，B0D3需要更名为HDAU,GFX0需要更名为IGPU.
3. HDAU注入的音频ID为3，hda-gfx值为onboard-2,IGPU的hda-gfx值也为onboard-2。

## SSDT注入
**注意：使用SSDT时，需要禁用ACPI中的change GFX0 to IGPU以及change B0D3 to HDAU,否则可能导致系统无法进入**
使用[MaciASL](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads/)新建一个dsl文件，复制以下代码后，编译生成aml文件，放入Clover\ACPI\patched目录下。
```
/*
 * Intel ACPI Component Architecture
 * AML/ASL+ Disassembler version 20161210-64(RM)
 * Copyright (c) 2000 - 2016 Intel Corporation
 * 
 * Disassembling to non-symbolic legacy ASL operators
 *
 * Disassembly of iASL83XrKo.aml, Sun Apr  1 20:23:01 2018
 *
 * Original Table Header:
 *     Signature        "SSDT"
 *     Length           0x000001E0 (480)
 *     Revision         0x01
 *     Checksum         0xE4
 *     OEM ID           "toleda"
 *     OEM Table ID     "am89hd55"
 *     OEM Revision     0x00003000 (12288)
 *     Compiler ID      "INTL"
 *     Compiler Version 0x20161210 (538317328)
 */
DefinitionBlock ("", "SSDT", 1, "toleda", "am89hd55", 0x00003000)
{
    External (_SB_.PCI0, DeviceObj)    // (from opcode)
    External (_SB_.PCI0.B0D3._ADR, UnknownObj)    // (from opcode)
    External (_SB_.PCI0.GFX0._ADR, UnknownObj)    // (from opcode)

    Method (XOSI, 1, NotSerialized)
    {
        Return (LEqual (Arg0, "Windows 2009"))
    }

    Scope (\_SB.PCI0)
    {
        Device (HDAU)
        {
            Name (_ADR, 0x00030000)  // _ADR: Address
            Method (_INI, 0, NotSerialized)  // _INI: Initialize
            {
                Store (Zero, \_SB.PCI0.B0D3._ADR)
            }

            Method (_DSM, 4, NotSerialized)  // _DSM: Device-Specific Method
            {
                If (LEqual (Arg2, Zero))
                {
                    Return (Buffer (One)
                    {
                         0x03                                           
                    })
                }

                Return (Package (0x04)
                {
                    "hda-gfx", 
                    Buffer (0x0A)
                    {
                        "onboard-2"
                    }, 

                    "layout-id", 
                    Buffer (0x04)
                    {
                         0x03, 0x00, 0x00, 0x00                         
                    }
                })
            }
        }

        Name (GFX0._STA, Zero)  // _STA: Status
        Device (IGPU)
        {
            Name (_ADR, 0x00020000)  // _ADR: Address
            Method (_INI, 0, NotSerialized)  // _INI: Initialize
            {
                Store (Zero, \_SB.PCI0.GFX0._ADR)
            }

            Method (_DSM, 4, NotSerialized)  // _DSM: Device-Specific Method
            {
                If (LEqual (Arg2, Zero))
                {
                    Return (Buffer (One)
                    {
                         0x03                                           
                    })
                }

                Return (Package (0x06)
                {
                    "AAPL,ig-platform-id", 
                    Buffer (0x04)
                    {
                         0x06, 0x00, 0x26, 0x16                         
                    }, 

                    "model", 
                    Buffer (0x17)
                    {
                        "Intel HD Graphics 5500"
                    }, 

                    "hda-gfx", 
                    Buffer (0x0A)
                    {
                        "onboard-2"
                    }
                })
            }
        }
    }

    Store ("ssdt-ami-8/9series_desktop_hd5500_hdmi_audio_v3.0 github.com/toleda", Debug)
}
```
**代码中注入的ID为16260006**
<!-- more --> 
## 使用Rehabman的[config_HD5300_5500_6000.plist](https://github.com/RehabMan/OS-X-Clover-Laptop-Config)打补丁
因为注入的ID为16260006，所以用Clover Configurator在Clover中的KextsToPatch应用以下补丁

```
Name:           com.apple.driver.AppleIntelBDWGraphicsFramebuffer
Comment:        HDMI-audio, port 0105, 0x16120003 0x16120005 0x16120006 0x16260006
Find:           01050B00 00040000 07050000
Replace:        01050B00 00080000 82000000
InfoPlistPatch: true

Name:           com.apple.driver.AppleIntelBDWGraphicsFramebuffer
Comment:        HDMI-audio, port 0204, 0x16120003 0x16120005 0x16120006 0x16260006
Find:           02040B00 00040000 07050000
Replace:        02040B00 00080000 82000000
InfoPlistPatch: true
```

## 正常驱动（如图）
![15224087280522](https://lh3.googleusercontent.com/-lajkHLs_tvA/Wr4dqs_kDBI/AAAAAAAAdl0/fEY4DI9G10E0TiJJNOL9101-BVrFLQI-ACHMYCw/I/15224087280522.jpg)

![](https://lh3.googleusercontent.com/-T_q26yoPJE8/Wr4d7DIVXHI/AAAAAAAAdl8/kuDKU1jLxWYtbfVnt6q17okKa9OZB1tHwCHMYCw/I/15224089397771.jpg)

