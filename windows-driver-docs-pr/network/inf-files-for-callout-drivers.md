---
title: 标注驱动程序的 INF 文件
description: 标注驱动程序的 INF 文件
keywords:
- Windows 筛选平台标注驱动程序 WDK，安装
- 标注驱动程序 WDK Windows 筛选平台，安装
- 安装标注驱动程序 WDK Windows 筛选平台
- INF 文件 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8406e46d7dce2d725b067161d77e789cc7b4831a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803525"
---
# <a name="inf-files-for-callout-drivers"></a>标注驱动程序的 INF 文件

Windows 筛选平台标注驱动程序由安装信息文件 (INF) 文件安装。 标注驱动程序的 INF 文件仅包含以下 INF 文件部分：

[**INF Version 节**](../install/inf-version-section.md)

[**INF SourceDisksNames 节**](../install/inf-sourcedisksnames-section.md)

[**INF SourceDisksFiles 节**](../install/inf-sourcedisksfiles-section.md)

[**INF DestinationDirs 节**](../install/inf-destinationdirs-section.md)

[**INF DefaultInstall 节**](../install/inf-defaultinstall-section.md)

[**INF DefaultInstall.Services 节**](../install/inf-defaultinstall-services-section.md)

[**INF Strings 节**](../install/inf-strings-section.md)

例如：

```INF
;
; Example callout driver INF file
;

[Version]
Signature = "$Windows NT$"
Provider = %Msft%
CatalogFile = "ExampleCalloutDriver.cat"
DriverVer = 01/15/05,1.0

[SourceDisksNames]
1 = %DiskName%

[SourceDisksFiles]
ExampleCalloutDriver.sys = 1

[DestinationDirs]
DefaultDestDir = 12 ; %windir%\system32\drivers
ExampleCalloutDriver.DriverFiles = 12 ; %windir%\system32\drivers

[DefaultInstall]
OptionDesc = %Description%
CopyFiles = ExampleCalloutDriver.DriverFiles

[DefaultInstall.Services]
AddService = %ServiceName%,,ExampleCalloutDriver.Service

[DefaultUninstall]
DelFiles = ExampleCalloutDriver.DriverFiles

[DefaultUninstall.Services]
DelService = ExampleCalloutDriver,0x200 ; SPSVCINST_STOPSERVICE

[ExampleCalloutDriver.DriverFiles]
ExampleCalloutDriver.sys,,,0x00000040 ; COPYFLG_OVERWRITE_OLDER_ONLY

[ExampleCalloutDriver.Service]
DisplayName = %ServiceName%
Description = %ServiceDesc%
ServiceType = 1  ; SERVICE_KERNEL_DRIVER
StartType = 0    ; SERVICE_BOOT_START
ErrorControl = 1 ; SERVICE_ERROR_NORMAL
ServiceBinary = %12%\ExampleCalloutDriver.sys

[Strings]
Msft = "Microsoft Corporation"
DiskName = "Example Callout Driver Installation Disk"
Description = "Example Callout Driver"
ServiceName = "ExampleCalloutDriver"
ServiceDesc = "Example Callout Driver"
```
