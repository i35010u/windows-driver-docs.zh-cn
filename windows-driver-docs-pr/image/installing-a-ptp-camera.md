---
title: 安装 PTP 相机
description: 安装 PTP 相机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c293af1bc81147aaa45b8ca11c952be61fda6a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793645"
---
# <a name="installing-a-ptp-camera"></a>安装 PTP 相机





如果照相机支持 PTP，只需插入设备即可将其作为 WIA 设备安装。 Microsoft PTP WIA 微型驱动程序将执行其余操作。

如果你有想要添加到 PTP 相机的附加或扩展，则需要创建一个 INF 文件。

请注意，INF 文件包含 *sti* 中的部分。 这允许 Microsoft 在需要时再对 *sti* 进行更新，而不会影响你的 inf 文件。

USB 设备工作组已为静止图像照相机分配类 ID 0x06。 在将来的 Windows 版本中，Microsoft 将提供一个 INF 文件，用于加载此类 ID 的 PTP 驱动程序作为 *兼容的 id* 匹配项。 这意味着，供应商仍可以通过交付包含 *硬件 ID* 的 INF 文件来加载自定义驱动程序。 Windows installer 的优先级比匹配类 ID 时的硬件 ID 更高。 如果 Windows 中未随附带有硬件 ID 的 INF 文件，则不会自动加载供应商驱动程序。 但是，CD 的自动运行程序可以调用 [**UpdateDriverForPlugAndPlayDevices**](/windows/win32/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa) 来轻松更新供应商驱动程序。

PTP 相机的示例 INF 文件：

```INF
; PTPCAMERA.INF  -- PTP Camera setup file
; Copyright (c) 2002 PTP Camera Company
; Manufacturer:  PTP Camera Company

[Version]
Signature=$WINDOWS NT$
Class=Image
ClassGUID={6bdd1fc6-810f-11d0-bec7-08002be2092f}
Provider=%Mfg%
DriverVer=06/26/2001,1.0
CatalogFile=wia.cat

[Manufacturer]
%Mfg%=Models

[Models]
%PTPCamera100.DeviceDesc%=PTP100, USB\VID_000&PID_0100

[PTP100]
Include=sti.inf
Needs=STI.PTPUSBSection

AddReg=PTP100.AddReg
DeviceData=PTP100.DeviceData
SubClass=StillImage
DeviceType=2
Capabilities=0x35
Events=PTP100.Events
ICMProfiles="sRGB Color Space Profile.icm"

[PTP100.Services]
Include=sti.inf
Needs=STI.USBSection.Services

[PTP100.DeviceData]
Model=PTP
QueryDeviceForName=1,1
Server=local
UI DLL=sti.dll
UI Class ID={4DB1AD10-3391-11D2-9A33-00C04FA36145}

[PTP100.Events]
Connected=%PTP.Connected%,{A28BBADE-64B6-11d2-A231-00C04FA31809},*
Disconnected=%PTP.Disconnected%,{143E4E83-6497-11d2-A231-00C04FA31809},*

[PTP100.AddReg]

[Strings]
Mfg="PTP Camera Company"
PTPCamera100.DeviceDesc="PTP Camera Model 100"
PTP.Connected="PTP Camera Connected"
PTP.Disconnected="PTP Camera Disconnected"
```

 

