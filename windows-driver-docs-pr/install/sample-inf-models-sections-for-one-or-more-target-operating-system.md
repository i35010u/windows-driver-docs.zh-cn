---
title: 目标操作系统的示例 INF 模型部分
description: 适用于一个或多个目标操作系统的示例 INF 模型部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5c34d4d30afbf89d795c0e858a27b7d4ff766e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787359"
---
# <a name="sample-inf-models-sections-for-one-or-more-target-operating-systems"></a>适用于一个或多个目标操作系统的示例 INF 模型部分


本主题演示了一个示例 INF 文件，该文件在各种操作系统和平台上安装驱动程序包。 此 INF 文件包含以下 INF 部分和指令：

- 具有各种 [**Inf *模型***](inf-models-section.md)的已装饰 [**inf 制造商部分**](inf-manufacturer-section.md)，适用于基于 x86 的系统上运行的设备安装：

  -   Microsoft Windows 2000

  -   Windows XP

  -   Windows Vista 或更高版本的 Windows

- 带有各种 [**Inf *模型***](inf-models-section.md)的已装饰 [**inf 制造商部分**](inf-manufacturer-section.md)，适用于运行 Windows Vista 或更高版本 windows 的基于 x86 和 AMD64 的系统上的设备安装。

- [**INF *DDInstall***](inf-ddinstall-section.md)和 [**_DDInstall_。**](inf-ddinstall-services-section.md)在基于 x86 和 AMD64 的目标系统上创建服务和注册表项的服务。

- [**INF CopyFiles 指令**](inf-copyfiles-directive.md) ，可将特定于平台的文件复制到基于 X86 和 AMD64 的目标系统。

```cpp
[Version]
Signature       = "$Windows NT$"
Class           = Net
ClassGUID       = {4d36e972-e325-11ce-bfc1-08002be10318}
Provider        = %Msft%
DriverVer       = 10/01/2002,6.0.5019.0

[Manufacturer]
%Msft%          = Msft, NTx86.6.0, NTamd64.6.0

; ----------------------------------------------------------------------
; Models Section
; ----------------------------------------------------------------------

;For Windows 2000 and Windows XP

[Msft]
%NetVMini.DeviceDesc%   = NetVMini.NTx86.ndi, root\NetVMini ; Root enumerated 
%NetVMini.DeviceDesc%   = NetVMini.NTx86.ndi, {b85b7c50-6a01-11d2-b841-00c04fad5171}\NetVMini ; Toaster Bus enumerated 

;For Windows Vista and later

[Msft.NTx86.6.0]
%NetVMini.DeviceDesc%    = NetVMini.NTx86.ndi, root\NetVMini ; Root enumerated 
%NetVMini.DeviceDesc%    = NetVMini.NTx86.ndi, {b85b7c50-6a01-11d2-b841-00c04fad5171}\NetVMini ; Toaster Bus enumerated 

[Msft.NTamd64.6.0]
%NetVMini.DeviceDesc%    = NetVMini.NTamd64.ndi, root\NetVMini ; Root enumerated 
%NetVMini.DeviceDesc%    = NetVMini.NTamd64.ndi, {b85b7c50-6a01-11d2-b841-00c04fad5171}\NetVMini ; Toaster Bus enumerated 

; ----------------------------------------------------------------------
; NT x86 DDInstall and DDInstall.Service Sections
; ----------------------------------------------------------------------
[NetVMini.NTx86.ndi]
Characteristics = 0x1 ; NCF_VIRTUAL
AddReg          = NetVMini.Reg
CopyFiles       = NetVMini.NTx86.CopyFiles

[NetVMini.NTx86.ndi.Services]
AddService      = NetVMini, 2, NetVMini.NTx86.Service

[NetVMini.NTx86.Service]
DisplayName     = %NetVMini.Service.DispName%
ServiceType     = 1 ;SERVICE_KERNEL_DRIVER
StartType       = 3 ;SERVICE_DEMAND_START
ErrorControl    = 1 ;SERVICE_ERROR_NORMAL
ServiceBinary   = %12%\netvmini_32.sys
LoadOrderGroup  = NDIS
AddReg          = TextModeFlags.Reg

; ----------------------------------------------------------------------
; NT x64 DDInstall and DDInstall.Service Sections
; ----------------------------------------------------------------------
[NetVMini.NTamd64.ndi]
Characteristics = 0x1 ; NCF_VIRTUAL
AddReg          = NetVMini.Reg
CopyFiles       = NetVMini.NTamd64.CopyFiles

[NetVMini.NTamd64.ndi.Services]
AddService      = NetVMini, 2, NetVMini.NTamd64.Service

[NetVMini.NTamd64.Service]
DisplayName     = %NetVMini.Service.DispName%
ServiceType     = 1 ;SERVICE_KERNEL_DRIVER
StartType       = 3 ;SERVICE_DEMAND_START
ErrorControl    = 1 ;SERVICE_ERROR_NORMAL
ServiceBinary   = %12%\netvmini_64.sys
LoadOrderGroup  = NDIS
AddReg          = TextModeFlags.Reg

; ----------------------------------------------------------------------
; Registry Section
; ----------------------------------------------------------------------
[NetVMini.Reg]
HKR,    ,               BusNumber,           0, "0" 
HKR, Ndi,               Service,             0, "NetVMini"
HKR, Ndi\Interfaces,    UpperRange,          0, "ndis5"
HKR, Ndi\Interfaces,    LowerRange,          0, "Ethernet"

[TextModeFlags.Reg]
HKR, , TextModeFlags,    0x00010001, 0x0001

; ----------------------------------------------------------------------
; Disk/FIle Sections
; ----------------------------------------------------------------------
[SourceDisksNames]
1 = %DiskId1%,"",,

[SourceDisksFiles]
netvmini_32.sys = 1,,
netvmini_64.sys = 1,,

[DestinationDirs]
DefaultDestDir             = 12
NetVMini.NTx86.CopyFiles   = 12
NetVMini.NTamd64.CopyFiles = 12

[NetVMini.NTx86.CopyFiles]
netvmini_32.sys,,,2

[NetVMini.NTamd64.CopyFiles]
netvmini_64.sys,,,2

; ----------------------------------------------------------------------
; Strings Section
; ----------------------------------------------------------------------
[Strings]
Msft                       = "Microsoft"      

NetVMini.DeviceDesc        = "Microsoft Virtual Ethernet Adapter"
NetVMini.Service.DispName  = "Microsoft Virtual Miniport"
DiskId1                    = "Microsoft Virtual Miniport Device Installation Disk #1"
```

 (*MultiOS*) 的示例 INF 文件（包括在 Windows 驱动程序工具包 (WDK) 中）演示了如何使用单个 INF 文件在多个版本的 Windows 上安装设备。 此文件位于 WDK 的 " *源 \\ 打印 \\ inf \\ MultiOS* " 目录中。

 

 





