---
title: 安装 ICC 配置文件
description: 安装 ICC 配置文件
ms.assetid: d9253ee8-c414-46a9-899f-46ae32cee41a
keywords:
- 颜色管理 WDK 打印，安装 ICC 配置文件
- ICC 配置文件 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bf3544b17d9316bd207f280513aaa4ded6b15b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366801"
---
# <a name="installing-icc-profiles"></a>安装 ICC 配置文件





若要安装的打印机 ICC 配置文件，文件必须列在[打印机 INF 文件](printer-inf-files.md)。

下面是会导致两个 ICC 配置文件文件安装的.inf 文件的示例。 请注意，配置文件将写入到颜色目录，它具有[打印机 dirid](printer-dirids.md) 66003 的值。

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








