---
title: XPSDrv 安装
description: XPSDrv 安装
ms.assetid: 0b5ef114-2862-46f9-bd32-ae09fa4e6a92
keywords:
- XPSDrv 的打印机驱动程序 WDK，安装
- INF 文件 WDK 打印，XPSDrv 的打印机驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33e6591271f42e4ff777b0daf4d6df9ccfc75d01
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390241"
---
# <a name="xpsdrv-installation"></a>XPSDrv 安装


若要安装正确的后台处理程序，XPSDrv 驱动程序必须包括以下：

-   [ **CopyFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff546346)指令所属的驱动程序 INF 文件必须引用[筛选器管道配置文件](filter-pipeline-configuration-file.md)。

-   需求指令必须引用 Xpsdrv.oem。 有关需求指令的详细信息，请参阅[ **INF DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)并[Inf 的源媒体](https://msdn.microsoft.com/library/windows/hardware/ff552302)。

-   如果配置模块基于 Unidrv，需求指令必须引用 Unidrv.oem 和 Xpsgpd.oem。 同样，如果 XPSDrv 驱动程序配置模块基于 PScript5，需求指令必须引用 Pscript.oem 和 Xpsppd.oem。

下面的代码示例说明了上述更改的 INF 文件。

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

 

 




