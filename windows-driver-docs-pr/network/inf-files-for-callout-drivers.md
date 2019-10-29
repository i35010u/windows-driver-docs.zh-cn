---
title: 标注驱动程序的 INF 文件
description: 标注驱动程序的 INF 文件
ms.assetid: 2cdaf6a4-3297-4081-a64e-7ab5dc74e7e8
keywords:
- Windows 筛选平台标注驱动程序 WDK，安装
- 标注驱动程序 WDK Windows 筛选平台，安装
- 安装标注驱动程序 WDK Windows 筛选平台
- INF 文件 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 585b153026c899a02da817315f43b1613d404746
ms.sourcegitcommit: 0e0dc5f080df541cbb13b87a49c5eb88f757d4b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72987836"
---
# <a name="inf-files-for-callout-drivers"></a>标注驱动程序的 INF 文件

Windows 筛选平台标注驱动程序由安装信息文件（INF）文件安装。 标注驱动程序的 INF 文件仅包含以下 INF 文件部分：

[**INF 版本部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)

[**INF SourceDisksNames 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)

[**INF SourceDisksFiles 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)

[**INF DestinationDirs 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)

[**INF DefaultInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-section)

[**INF DefaultInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)

[**INF 字符串部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)

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
