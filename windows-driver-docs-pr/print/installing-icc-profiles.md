---
title: 安装 ICC 配置文件
description: 安装 ICC 配置文件
keywords:
- 颜色管理 WDK 打印，安装 ICC 配置文件
- ICC 配置文件 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc22d4c3ae40d62fef47860ba94af6ceb196521b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835655"
---
# <a name="installing-icc-profiles"></a>安装 ICC 配置文件





若要为打印机安装 ICC 配置文件，这些文件必须在 [打印机 INF 文件](printer-inf-files.md)中列出。

下面是导致安装两个 ICC 配置文件的 .inf 文件的示例。 请注意，配置文件将写入颜色目录，其 [打印机 dirid](printer-dirids.md) 值为66003。

```cpp
[Version]
Signature="$Windows NT$"
Provider="My Company" 
ClassGUID={4D36E979-E325-11CE-BFC1-08002BE10318}
Class=Printer

[My Company]
"My printer model" = MYDRIVER,My_Printer_Model

[MYDRIVER]
DriverFile=DRVR.DRV
DataFile=DRVR.DRV
CopyFiles=@DRVR.DRV,MY_COLOR_PROFILES
DataSection=MYDATA

[MYDATA]
HelpFile=DRVR.HLP
DefaultDataType=EMF

[MY_COLOR_PROFILES]
profile1.icm
profile2.icm

[DestinationDirs]
DefaultDestDir=11
MY_COLOR_PROFILES =66003
```








