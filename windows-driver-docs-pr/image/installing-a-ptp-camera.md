---
title: 安装 PTP 相机
description: 安装 PTP 相机
ms.assetid: bf18a245-1344-47f1-83bc-3c369627bcdf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3b05221eb1d8d2e4d9e828fd6de84c5fb4cfdc9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378945"
---
# <a name="installing-a-ptp-camera"></a>安装 PTP 相机





如果您的照相机支持 PTP，您需要做是若要获取其安装为 WIA 的设备将设备插入。 Microsoft PTP WIA 微型驱动程序将完成其余部分。

如果必须添加件或你想要添加到 PTP 摄像机的扩展，您需要创建一个 INF 文件。

请注意，INF 文件包含从部分*sti.inf*。 这样，Microsoft 使将来的更新*sti.inf*时需要而不会影响您的 INF 文件。

USB 设备处理组已分配类 ID 0x06:sp 静止图像照相机。 在将来的 Windows 版本中，Microsoft 将发布为为此类 ID 加载 PTP 驱动程序的 INF 文件*兼容 ID*匹配。 这意味着供应商仍可以寄送包含的 INF 文件加载自定义驱动程序*硬件 ID*。 Windows 安装程序将更高的优先级上匹配的硬件 ID 比匹配类 id。 如果在 Windows 中不提供硬件 id 的 INF 文件，供应商驱动程序不会自动加载。 但是，CD 自动运行程序可以调用[ **UpdateDriverForPlugAndPlayDevices** ](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)轻松地更新供应商驱动程序。

PTP 照相机的示例 INF 文件：

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

 

 




