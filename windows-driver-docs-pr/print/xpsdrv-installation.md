---
title: XPSDrv 安装
description: XPSDrv 安装
keywords:
- XPSDrv 打印机驱动程序 WDK，安装
- INF 文件 WDK 打印，XPSDrv 打印机驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58c28dac8ef71f2786a1d29b40c845b4cc2f7fa8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785717"
---
# <a name="xpsdrv-installation"></a>XPSDrv 安装


为正确安装后台处理程序，XPSDrv 驱动程序必须包括以下各项：

-   驱动程序 INF 文件的 [**CopyFiles**](../install/inf-copyfiles-directive.md) 指令必须引用 [筛选器管道配置文件](filter-pipeline-configuration-file.md)。

-   需要指令必须引用 Xpsdrv. oem。 有关 "需要" 指令的详细信息，请参阅 [**Inf DDInstall 部分**](../install/inf-ddinstall-section.md) 和 Inf [源媒体](../install/source-media-for-inf-files.md)。

-   如果配置模块基于 Unidrv，则需要指令必须引用 Unidrv 和 Xpsgpd。 同样，如果 XPSDrv 驱动程序配置模块基于 PScript5，则需要指令必须引用 Pscript 和 Xpsppd。

下面的代码示例阐释了前面更改的 INF 文件。

```cpp
[Version]
Signature="$Windows NT$"
Provider=%MS%
ClassGUID={4D36E979-E325-11CE-BFC1-08002BE10318}
Class=Printer
CatalogFile=ntprint.cat
DriverVer=10/11/2005,6.0.5242.0

[Manufacturer]
Microsoft

[Microsoft]
"XPSDrv Sample Driver" = INSTALL_XDSMPL_FILTERS

[INSTALL_XDSMPL_FILTERS]
CopyFiles=XPSDrvSample,ConfigPlugin,COLORPROFILES
DriverFile=mxdwdrv.dll
ConfigFile=unidrvui.dll
HelpFile=unidrv.HLP 
DataFile=XDSmpl.GPD
Include=NTPRINT.INF
Needs=UNIDRV.OEM, XPSGPD.OEM, XPSDRV.OEM
ICMProfiles=xdwscRGB.cdmp

[XPSDrvSample]
xdsmpl-pipelineconfig.xml
...
```

 

