---
title: 查看 INF 文件
description: 查看 INF 文件
keywords:
- INF 文件 WDK 设备安装，结构
- INF 文件 WDK 设备安装，部分
- 部分 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 115223d58771279eee0bf540ec7bb79f40d17830
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836429"
---
# <a name="looking-at-an-inf-file"></a>查看 INF 文件





下面的示例显示了系统提供的类安装程序的 INF 文件中的选定片段，以显示任何 INF 文件是由多个行组成的，其中每个行都包含零个或多个行，其中一些是引用其他由 INF 编写器定义的部分的项：

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

之前 INF 文件中的几个部分具有系统定义的名称，如 **Version**、 **DestinationDirs**、 **Manufacturer** 和 **string**。 一些命名部分（如 **版本**、 **DestinationDirs** 和 **字符串** ）只有简单的条目。 其他人引用其他 INF 写入器定义的部分，如 " **制造商** " 部分的前一示例中所示。

请注意，在前面的示例中，从 **制造商** 部分开始，针对鼠标设备驱动程序安装的相关部分的隐含层次结构。 下图显示了 INF 文件中某些部分的层次结构。

![说明 inf 文件中各节的示例层次结构的关系图](images/inf-sections.png)

对于 INF 文件的隐含层次结构，请注意以下事项：

- 制造商部分中的每个 **%** <em>xx</em>制造 <strong>%</strong> 条目都引用了每个制造商的 *型号* (StdMfg，) MSMfg 在 INF 文件中的其他位置。 **Manufacturer**

  上一示例中的条目使用%*strkey*% 令牌。

- 每个 *模型* 部分指定了一些条目数;在示例中，它们为 **%** <em>xxx</em>。DeviceDesc <strong>%</strong> 标记。

  每个此类 **%** <em>xxx</em>。DeviceDesc <strong>%</strong> 令牌引用了某些每个模型的 *DDInstall* 部分 (Ser_Inst 和 Inp_Inst) 对于该制造商的产品系列，每个条目标识单个设备 (\* PNP0F0C 和 \* PNP0F0D，因此此处所示) 或一组兼容型号的设备。

- 接下来，每个此类 *DDInstall* *Xxx* _Inst 部分都可以具有某些系统定义的扩展插件，并且/或可以包含引用其他由 INF 编写器定义的部分的指令。 例如，在前面的示例中显示为片段的完整 INF 文件也有一个 Ser_Inst <strong>。服务</strong> 部分及其 Ser_Inst 部分中有一个 **CopyFiles** 指令，该指令引用此 INF 文件中其他位置的 Ser_CopyFiles 部分。

 

 





