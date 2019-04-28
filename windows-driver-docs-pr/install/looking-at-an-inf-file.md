---
title: 查看 INF 文件
description: 查看 INF 文件
ms.assetid: 4d9d5f28-b643-4369-8bf8-94703e8926d2
keywords:
- INF 文件 WDK 设备安装，结构
- INF 文件 WDK 设备安装，部分
- 部分 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dfc3fb3a6eb63d47e5d829be12a0c3b1e73ee2c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346825"
---
# <a name="looking-at-an-inf-file"></a>查看 INF 文件





下面的示例演示从系统提供的类安装程序的 INF 文件，以显示如何任何 INF 文件个部分组成，其中每个包含零个或多个行，其中一些为引用其他条目 INF 编写器定义的所选的片段部分：

```cpp
[Version]
Signature="$Windows NT$"
Class=Mouse
ClassGUID={4D36E96F-E325-11CE-BFC1-08002BE10318}
Provider=%Provider% ; defined later in Strings section
DriverVer=09/28/1999,5.00.2136.1
 
[DestinationDirs]
DefaultDestDir=12 ; DIRID_DRIVERS
 
; ... [ControlFlags] section omitted here
 
[Manufacturer]
%StdMfg%    =StdMfg         ; (Standard types)
%MSMfg%     =MSMfg          ; Microsoft
; ... %otherMfg% entries omitted here
 
[StdMfg]  ; per-Manufacturer Models section 
; Std serial mouse
%*pnp0f0c.DeviceDesc%= Ser_Inst,*PNP0F0C,SERENUM\PNP0F0C,SERIAL_MOUSE
; Std InPort mouse
%*pnp0f0d.DeviceDesc%      = Inp_Inst,*PNP0F0D
     ; ... more StdMfg entries and following
     ; MSMfg and xxMfg Models sections omitted here
 
     ; per-Models DDInstall (Ser_Inst, Inp_Inst, etc.)
     ; sections also omitted here
 
[Strings] 
; where INF %strkey% tokens are defined as user-visible (and
; possibly as locale-specific) strings.
Provider = "Microsoft"
; ...
StdMfg   = "(Standard mouse types)"
MSMfg    = "Microsoft"
 
; ...
*pnp0f0c.DeviceDesc   = "Standard Serial Mouse"
*pnp0f0d.DeviceDesc   = "InPort Adapter Mouse"
; ... 
HID\Vid_045E&Pid_0009.DeviceDesc = "Microsoft USB Intellimouse"
; ... 
```

以前的 INF 文件中的几个部分提供的系统定义的名称，如**版本**， **DestinationDirs**，**制造商**，和**字符串**. 一些命名等部分**版本**， **DestinationDirs**，并**字符串**包含仅简单的条目。 其他引用 INF 编写器定义的其他部分，如前面的示例中所示**制造商**部分。

请注意对于开头的鼠标设备驱动程序安装的相关章节的隐式层次结构**制造商**上一示例中的部分。 下图显示 INF 文件中的某些部分在层次结构。

![说明的 inf 文件中的部分示例层次结构的关系图](images/inf-sections.png)

请注意以下有关 INF 文件的隐式层次结构：

- 每个**%** <em>xx</em>制造业<strong>%</strong> 中的条目**制造商**部分引用每个-制造商*模型*INF 文件中的其他位置 （StdMfg，MSMfg） 部分。

  上一示例中的条目使用 %*strkey*%令牌。

- 每个*模型*部分指定一定数量的条目; 在本例中，它们是**%** <em>xxx</em>。DeviceDesc<strong>%</strong>令牌。

  每个此类**%** <em>xxx</em>。DeviceDesc<strong>%</strong>令牌引用一定数量的每个模型*DDInstall*对于该制造商的产品行，其中每个条目的部分 （Ser_Inst 和 Inp_Inst）标识单个设备 (\*PNP0F0C 和\*PNP0F0D，因此"DeviceDesc"如下所示) 或一组兼容型号的设备。

- 每个此类*DDInstall*-类型*Xxx*_Inst 部分中，又可以追加某些系统定义的扩展和/或可以包含引用 INF 编写器定义的其他部分的指令。 例如，为上一示例中的片段所示的完整 INF 文件还具有 Ser_Inst<strong>。服务</strong>部分中，并且其 Ser_Inst 部分已**CopyFiles**指令，它引用此 INF 文件中的其他位置 Ser_CopyFiles 部分。

 

 





