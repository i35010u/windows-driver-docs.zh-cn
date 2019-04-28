---
title: INF Driver-Version 条目
description: INF Driver-Version 条目
ms.assetid: 092cd9ed-8988-4ffd-9958-1267f3c52819
keywords:
- 版本编号 WDK 音频
- INF 文件 WDK 音频
- 音频的微型端口驱动程序 WDK，版本号
- 微型端口驱动程序 WDK 音频，版本号
- 音频驱动程序 WDK，版本号
- 驱动程序版本数字 WDK 音频
- INF DriverVer 指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 545ce33436a4870432329a2c2394cc2197bab446
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333544"
---
# <a name="inf-driver-version-entry"></a>INF Driver-Version 条目


## <span id="inf_driver_version_entry"></span><span id="INF_DRIVER_VERSION_ENTRY"></span>


驱动程序包中的 INF 文件指定的驱动程序的情况下 INF 安装的驱动程序版本信息。 在文件中的版本信息标识驱动程序包作为一个整体，相反[内部和外部版本号](internal-and-external-version-numbers.md)包内的单独的驱动程序文件。

该文件指定每个驱动程序中的日期和版本编号[ **INF DriverVer 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547394)具有以下格式：

**DriverVer**= *mm* / *dd* / *yyyy*\[,*x*.*y*.*v*.*z*\]

Date 参数*mm*/*dd*/*yyyy*两位数字代码组成*mm*，两位数字的日期代码*dd*，和四位数年份代码*yyyy*。 此参数指定的驱动程序包的日期，适用于所有驱动程序文件，其中包括 INF 文件。 连字符 （-） 可用作替代斜杠 （/） 的日期字段分隔符。 操作系统使用**DriverVer**日期来执行驱动程序版本比较时驱动程序的两个版本之间进行选择。 此日期也将出现在**驱动程序日期**通过设备管理器中显示的值。

可选的版本号*x*。*y*。*v*。*z* ，该方法显示在括号内更高版本，仅出于显示目的使用 (例如，在**驱动程序版本**通过设备管理器中显示的数字)。 操作系统不使用的驱动程序选择此值。 在编译时驱动程序文件，请确保内部版本号中指定*FILEVERSION*中的驱动程序的资源文件匹配的参数**DriverVer** INF 中的版本编号文件。

当操作系统搜索驱动程序时，它选择的驱动程序有较新**DriverVer**驱动程序通过更早日期的日期。 如果一个 INF 文件没有**DriverVer**条目或未签名，操作系统将应用默认的日期的 00 00/0000。

在 Windows 2000 中，Windows XP 和更高版本，必须提供一个驱动程序包的 INF 文件**DriverVer**指令。

 

 




