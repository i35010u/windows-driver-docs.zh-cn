---
title: 示例 INF 适用目标操作系统于模型的各部分
description: 示例 INF 模型部分用于一个或多针对操作系统
ms.assetid: bc1d9a5f-573f-4773-8716-8ac53478d0ee
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1a11f39ddd9ea284eae37c9bcf6971a2b42b77a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522335"
---
# <a name="sample-inf-models-sections-for-one-or-more-target-operating-systems"></a>示例 INF 模型部分用于一个或多针对操作系统


本主题说明在各种操作系统和平台安装驱动程序包的示例 INF 文件。 此 INF 文件具有以下 INF 部分和指令：

- 修饰[ **INF 制造商部分**](inf-manufacturer-section.md)的各种[ **INF*模型*部分**](inf-models-section.md)设备正在运行的基于 x86 的系统上安装：

  -   Microsoft Windows 2000

  -   Windows XP

  -   Windows Vista 或更高版本的 Windows

- 修饰[ **INF 制造商部分**](inf-manufacturer-section.md)的各种[ **INF*模型*部分**](inf-models-section.md)设备x86-和 AMD64 安装-基于在运行 Windows Vista 或更高版本的 Windows 的系统。

- [ **INF *DDInstall***  ](inf-ddinstall-section.md)并[ * **DDInstall *。服务**](inf-ddinstall-services-section.md)目标 x86-和 AMD64 上创建的服务和注册表项-基于系统。

- [**INF CopyFiles 指令**](inf-copyfiles-directive.md) ，将特定于平台的文件复制到目标 x86-和 AMD64-基于系统。

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

示例 INF 文件 (*MultiOS.inf*)，后者包含在 Windows Driver Kit (WDK) 中，演示如何使用单个的 INF 文件在多个版本的 Windows 上安装的设备。 此文件位于*src\\打印\\inf\\MultiOS* WDK 的目录。

 

 





