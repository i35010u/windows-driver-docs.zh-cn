---
title: PSHED 插件的 INF 文件
description: PSHED 插件的 INF 文件
ms.assetid: 60bb9902-c558-4ee1-9b33-1a08885e7c06
keywords:
- PSHED 插件 WDK WHEA、 INF 文件
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，INF 文件
- INF 文件 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 604861b275a238d875dd06be3b32fb929a0159d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575391"
---
# <a name="inf-files-for-pshed-plug-ins"></a>PSHED 插件的 INF 文件


情况下，安装插件 PSHED[信息 (INF) 文件](https://msdn.microsoft.com/library/windows/hardware/ff547402)。 PSHED 插件的 INF 文件包含以下标准的 INF 文件部分：

[**INF 版本部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)

[**INF SourceDisksNames 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547478)

[**INF SourceDisksFiles 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547472)

[**INF DestinationDirs 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547383)

[**INF 制造商部分**](https://msdn.microsoft.com/library/windows/hardware/ff547454)

[**INF*模型*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547456)

[**INF *DDInstall*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**INF *DDInstall*。服务部分**](https://msdn.microsoft.com/library/windows/hardware/ff547349)

[**INF 字符串部分**](https://msdn.microsoft.com/library/windows/hardware/ff547485)

内[ **INF*模型*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547456)，平台供应商可以使用任何[硬件标识符 (ID)](https://msdn.microsoft.com/library/windows/hardware/ff546152)为 PSHED 插件。 通过使用指定 ID 的硬件*hw id*中的条目*模型*部分，并可以是在 ACPI 名称空间或另一个设备命名空间中的硬件 ID。 此外可以指定供应商[兼容 ID](https://msdn.microsoft.com/library/windows/hardware/ff539950)值为*PNP0C33*。 此兼容 ID 用于定义为与 Microsoft 兼容硬件错误设备。 供应商通过使用指定的兼容 ID*兼容 id*中的条目*模型*部分。

PSHED 插件的 INF 文件还必须包括[ **AddReg** ](https://msdn.microsoft.com/library/windows/hardware/ff546320)指令，它引用添加到项目文件中的某个部分**系统**\\ **CurrentControlSet**\\**控件**\\**PSHED**\\**插件**密钥在注册表中。 此条目会通知 PSHED 系统中安装了插件 PSHED。 这允许 PSHED 以验证所有已安装的 PSHED 插件已成功加载每个系统启动的时间。

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

 

 




