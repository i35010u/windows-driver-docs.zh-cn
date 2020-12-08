---
title: INF Driver-Version 条目
description: INF Driver-Version 条目
keywords:
- 版本号 WDK 音频
- INF 文件 WDK 音频
- 音频微型端口驱动程序 WDK，版本号
- 微型端口驱动程序 WDK 音频，版本号
- 音频驱动程序 WDK，版本号
- 驱动程序版本号 WDK 音频
- INF DriverVer 指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04d58afe3ba7e89fddf9df3cd393057b89bb750a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784743"
---
# <a name="inf-driver-version-entry"></a>INF Driver-Version 条目


## <span id="inf_driver_version_entry"></span><span id="INF_DRIVER_VERSION_ENTRY"></span>


驱动程序包中的 INF 文件指定 INF 所安装的驱动程序的驱动程序版本信息。 文件中的版本信息以整体形式标识驱动程序包，与包内单个驱动程序文件的 [内部和外部版本号](internal-and-external-version-numbers.md) 不同。

该文件使用以下格式指定 [**INF DriverVer 指令**](../install/inf-driverver-directive.md) 中每个驱动程序的日期和版本号：

**DriverVer** = *mm*  / *dd*  / *yyyy* \[ ，*x*。*y*。*v*。*z*\]

Date 参数 *mm* / *dd* / *yyyy* 包含两位数的月份代码 *mm*、两位数的日期代码 *dd* 和四位数年份代码 *yyyy*。 此参数指定驱动程序包的日期并应用于所有驱动程序文件，包括 INF 文件。 连字符 ( ) 可用作日期字段分隔符，以代替斜杠 (/) 。 在两个版本的驱动程序之间进行选择时，操作系统使用 **DriverVer** 日期来执行驱动程序版本比较。 此日期还会显示在设备管理器显示的 " **驱动程序日期** " 值中。

可选的版本号 *x*。*y*。*v*。*z* （如上所示）仅用于显示目的，例如，在设备管理器) 显示的 **驱动程序版本号** 中 (。 操作系统不会将此值用于驱动程序选择。 编译驱动程序文件时，请确保在驱动程序的资源文件中的 *FILEVERSION* 参数中指定的内部版本号与 INF 文件中的 **DriverVer** 版本号匹配。

当操作系统搜索驱动程序时，它会选择一个驱动程序，该驱动程序的 **DriverVer** 日期比之前日期更近。 如果 INF 文件没有 **DriverVer** 项或未签名，则操作系统将应用默认日期00/00/0000。

在 Windows 2000、Windows XP 及更高版本中，驱动程序包的 INF 文件必须提供 **DriverVer** 指令。

 

