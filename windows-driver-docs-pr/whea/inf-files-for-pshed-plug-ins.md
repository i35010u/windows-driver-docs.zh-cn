---
title: PSHED 插件的 INF 文件
description: PSHED 插件的 INF 文件
ms.assetid: 60bb9902-c558-4ee1-9b33-1a08885e7c06
keywords:
- PSHED 插件 WDK WHEA，INF 文件
- 平台特定硬件错误驱动程序插件 WDK WHEA，INF 文件
- INF 文件 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 382793bdbfde473d2188b0720b8252cc0121abda
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733092"
---
# <a name="inf-files-for-pshed-plug-ins"></a>PSHED 插件的 INF 文件


PSHED 插件由 [ (INF) 文件的信息](../install/overview-of-inf-files.md)安装。 用于 PSHED 插件的 INF 文件包含以下标准 INF 文件部分：

[**INF 版本部分**](../install/inf-version-section.md)

[**INF SourceDisksNames 节**](../install/inf-sourcedisksnames-section.md)

[**INF SourceDisksFiles 节**](../install/inf-sourcedisksfiles-section.md)

[**INF DestinationDirs 节**](../install/inf-destinationdirs-section.md)

[**INF Manufacturer 节**](../install/inf-manufacturer-section.md)

[**INF *型号* 部分**](../install/inf-models-section.md)

[**INF *DDInstall* 部分**](../install/inf-ddinstall-section.md)

[**INF *DDInstall*。服务部分**](../install/inf-ddinstall-services-section.md)

[**INF Strings 节**](../install/inf-strings-section.md)

在 " [**INF *模型* " 部分**](../install/inf-models-section.md)中，平台供应商可将任何 [硬件标识符 (ID) ](../install/hardware-ids.md) 用于 PSHED 插件。 硬件 ID 是使用 "*模型*" 部分中的 " *hw-ID* " 条目指定的，可以是 ACPI 命名空间或其他设备命名空间中的硬件 id。 供应商还可以指定值为*PNP0C33*的[兼容 ID](../install/compatible-ids.md) 。 此兼容 ID 用于定义与 Microsoft 兼容的硬件错误设备。 供应商通过使用 "*模型*" 部分中的 "*兼容-ID* " 条目来指定兼容 id。

PSHED 插件的 INF 文件还必须包括一个[**AddReg**](../install/inf-addreg-directive.md)指令，该指令引用文件中的一个部分，该部分将条目添加到注册表中的**System** \\ **CurrentControlSet** \\ **Control** \\ **PSHED** \\ **插件**项。 此条目通知 PSHED 已在系统中安装了 PSHED 插件。 这允许 PSHED 验证每次启动系统时是否已成功加载所有已安装的 PSHED 插件。

例如：

```cpp
;
; Example PSHED plug-in INF file
;

[Version]
Signature = "$Windows NT$"
Provider = %Msft%
CatalogFile = "ExamplePSHEDPlugin.cat"
DriverVer = 01/01/06,1.0

[SourceDiskNames]
1 = %DiskName%

[SourceDiskFiles]
%FileName% = 1

[DestinationDirs]
DefaultDestDir = 12 ; %SystemRoot%\system32\drivers
ExamplePSHEDPlugin.DriverFiles = 12 ; %SystemRoot%\system32\drivers

[Manufacturer]
%Msft% = Microsoft

[Microsoft]
%DeviceDesc% = ExamplePSHEDPluginInstall,%DeviceId%

[ExamplePSHEDPluginInstall]
OptionDesc = %Description%
CopyFiles = ExamplePSHEDPlugin.DriverFiles
AddReg = ExamaplePSHEDPlugin.AddReg

[ExamplePSHEDPluginInstall.Services]
AddService = %ServiceName%,,ExamplePSHEDPlugin.Service

[ExamplePSHEDPlugin.DriverFiles]
%FileName%,,,0x00000040 ; COPYFLG_OVERWRITE_OLDER_ONLY

[ExamplePSHEDPlugin.AddReg]
HKLM,%PSHEDControlPath%,%ServiceName%,0x00000000,%FileName%

[ExamplePSHEDPlugin.Service]
DisplayName = %ServiceName%
Description = %ServiceDesc%
ServiceType = 1  ; SERVICE_KERNEL_DRIVER
StartType = 3    ; SERVICE_DEMAND_START
ErrorControl = 1 ; SERVICE_ERROR_NORMAL
ServiceBinary = %12%\%FileName%

[Strings]
%Msft% = "Microsoft Corporation"
%DiskName% = "Example PSHED Plug-In Installation Disk"
%FileName% = "ExamplePSHEDPlugin.sys"
%DeviceDesc% = "Example PSHED Plug-In Device"
%DeviceId% = "ACPI\PSHEDPI"
%Description% = "Example PSHED Plug-In"
%ServiceName% = "ExamplePSHEDPlugin"
%ServiceDesc% = "Example PSHED Plug-In"
%PSHEDControlPath% = "System\CurrentControlSet\Control\PSHED\Plugins"
```

