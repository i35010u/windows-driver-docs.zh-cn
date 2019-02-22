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
ms.openlocfilehash: 2e694073d8d3d7c3f80d951f412a0649997b46ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544220"
---
# <a name="inf-files-for-callout-drivers"></a>标注驱动程序的 INF 文件


通过安装程序信息文件 (INF) 文件安装 Windows 筛选平台标注驱动程序。 标注驱动程序的 INF 文件包含仅以下 INF 文件部分：

[**INF 版本部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)

[**INF SourceDisksNames 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547478)

[**INF SourceDisksFiles 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547472)

[**INF DestinationDirs 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547383)

[**INF DefaultInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547356)

[**INF DefaultInstall.Services 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547360)

[**INF 字符串部分**](https://msdn.microsoft.com/library/windows/hardware/ff547485)

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
%Msft% = "Microsoft Corporation"
%DiskName% = "Example Callout Driver Installation Disk"
%Description% = "Example Callout Driver"
%ServiceName% = "ExampleCalloutDriver"
%ServiceDesc% = "Example Callout Driver"
```
