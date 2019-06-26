---
title: 远程 NDIS INF 模板
description: 远程 NDIS INF 模板
ms.assetid: bbbd3aef-230f-4286-bea2-bb583789865e
keywords:
- 远程 NDIS WDK 网络、 INF 模板
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a4f072409e2ed1b618ef81b7d12a36fc3e8b2fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361146"
---
# <a name="remote-ndis-inf-template"></a>远程 NDIS INF 模板





Microsoft 提供的 NDIS 微型端口驱动程序 Rndismp.sys，实现远程 NDIS 消息组并与泛型总线传输驱动程序，它又与其相应的总线驱动程序进行通信。 此 NDIS 微型端口驱动程序是实现并由 Microsoft 维护并作为所有受支持的 Windows 版本的一部分分发。 可以在 %systemroot%中找到它\\System32\\驱动程序目录。

若要使用 USB 设备的远程 NDIS 驱动程序，IHV 必须提供 INF 文件根据以下模板之一：

-   [NDIS 5.1 RNDIS INF 模板 (Windows XP 及更高版本)](#rndis-inf-template-for-ndis-51-windows-xp-and-later)
-   [NDIS 6.0 (Windows 7 及更高版本) 的 RNDIS INF 模板](#rndis-inf-template-for-ndis-60-windows-7-and-later)

### <a name="rndis-inf-template-for-ndis-51-windows-xp-and-later"></a>NDIS 5.1 RNDIS INF 模板 (Windows XP 及更高版本)

```INF
; Remote NDIS template device setup file
; Copyright (c) Microsoft Corporation
;
; This is the template for the INF installation script 
; for the RNDIS-over-USB host driver.
; This INF works for Windows XP SP2, Windows XP x64, 
; Windows Server 2003 SP1 x86, x64, and ia64, and 
 ; Windows Vista x86 and x64.
; This INF will work with Windows XP, Windows XP SP1, 
; and Windows 2003 after applying specific hotfixes.

[Version]
Signature           = "$Windows NT$"
Class               = Net
ClassGUID           = {4d36e972-e325-11ce-bfc1-08002be10318}
Provider            = %Microsoft%
DriverVer           =06/21/2006,6.0.6000.16384
;CatalogFile        = device.cat

[Manufacturer]
%Microsoft%         = RndisDevices,NTx86,NTamd64,NTia64

; Decoration for x86 architecture
[RndisDevices.NTx86]
%RndisDevice%    = RNDIS.NT.5.1, USB\VID_xxxx&PID_yyyy

; Decoration for x64 architecture
[RndisDevices.NTamd64]
%RndisDevice%    = RNDIS.NT.5.1, USB\VID_xxxx&PID_yyyy

; Decoration for ia64 architecture
[RndisDevices.NTia64]
%RndisDevice%    = RNDIS.NT.5.1, USB\VID_xxxx&PID_yyyy

;@@@ This is the common setting for setup
[ControlFlags]
ExcludeFromSelect=*

; DDInstall section
; References the in-build Netrndis.inf
[RNDIS.NT.5.1]
Characteristics = 0x84   ; NCF_PHYSICAL + NCF_HAS_UI
BusType         = 15
; NEVER REMOVE THE FOLLOWING REFERENCE FOR NETRNDIS.INF
include         = netrndis.inf
needs           = Usb_Rndis.ndi
AddReg          = Rndis_AddReg_Vista

; DDInstal.Services section
[RNDIS.NT.5.1.Services]
include     = netrndis.inf
needs       = Usb_Rndis.ndi.Services

; Optional registry settings. You can modify as needed.
[RNDIS_AddReg_Vista] 
HKR, NDI\params\VistaProperty, ParamDesc,  0, %Vista_Property%
HKR, NDI\params\VistaProperty, type,       0, "edit"
HKR, NDI\params\VistaProperty, LimitText,  0, "12"
HKR, NDI\params\VistaProperty, UpperCase,  0, "1"
HKR, NDI\params\VistaProperty, default,    0, " "
HKR, NDI\params\VistaProperty, optional,   0, "1"

; No sys copyfiles - the sys files are already in-build 
; (part of the operating system).

; Modify these strings for your device as needed.
[Strings]
Microsoft             = "Microsoft Corporation"
RndisDevice           = "Remote NDIS based Device"
Vista_Property        = "Optional Vista Property"
```

### <a name="rndis-inf-template-for-ndis-60-windows-7-and-later"></a>NDIS 6.0 (Windows 7 及更高版本) 的 RNDIS INF 模板

```INF
; Remote NDIS template device setup file
; Copyright (c) Microsoft Corporation
;
; This is the template for the INF installation script  for the RNDIS-over-USB
; host driver that leverages the newer NDIS 6.x miniport (rndismp6.sys) for
; improved performance. This INF works for Windows 7, Windows Server 2008 R2,
; and later operating systems on x86, amd64 and ia64 platforms.

[Version]
Signature           = "$Windows NT$"
Class               = Net
ClassGUID           = {4d36e972-e325-11ce-bfc1-08002be10318}
Provider            = %Microsoft%
DriverVer           = 07/21/2008,6.0.6000.16384
;CatalogFile        = device.cat

[Manufacturer]
%Microsoft%         = RndisDevices,NTx86,NTamd64,NTia64

; Decoration for x86 architecture
[RndisDevices.NTx86]
%RndisDevice%    = RNDIS.NT.6.0, USB\VID_xxxx&PID_yyyy

; Decoration for x64 architecture
[RndisDevices.NTamd64]
%RndisDevice%    = RNDIS.NT.6.0, USB\VID_xxxx&PID_yyyy

; Decoration for ia64 architecture
[RndisDevices.NTia64]
%RndisDevice%    = RNDIS.NT.6.0, USB\VID_xxxx&PID_yyyy

;@@@ This is the common setting for setup
[ControlFlags]
ExcludeFromSelect=*

; DDInstall section
; References the in-build Netrndis.inf
[RNDIS.NT.6.0]
Characteristics = 0x84   ; NCF_PHYSICAL + NCF_HAS_UI
BusType         = 15
; NEVER REMOVE THE FOLLOWING REFERENCE FOR NETRNDIS.INF
include         = netrndis.inf
needs           = usbrndis6.ndi
AddReg          = Rndis_AddReg
*IfType            = 6    ; IF_TYPE_ETHERNET_CSMACD.
*MediaType         = 16   ; NdisMediumNative802_11
*PhysicalMediaType = 14   ; NdisPhysicalMedium802_3

; DDInstal.Services section
[RNDIS.NT.6.0.Services]
include     = netrndis.inf
needs       = usbrndis6.ndi.Services

; Optional registry settings. You can modify as needed.
[RNDIS_AddReg] 
HKR, NDI\params\RndisProperty, ParamDesc,  0, %Rndis_Property%
HKR, NDI\params\RndisProperty, type,       0, "edit"
HKR, NDI\params\RndisProperty, LimitText,  0, "12"
HKR, NDI\params\RndisProperty, UpperCase,  0, "1"
HKR, NDI\params\RndisProperty, default,    0, " "
HKR, NDI\params\RndisProperty, optional,   0, "1"

; No sys copyfiles - the sys files are already in-build 
; (part of the operating system).

; Modify these strings for your device as needed.
[Strings]
Microsoft             = "Microsoft Corporation"
RndisDevice           = "Remote NDIS6 based Device"
Rndis_Property         = "Optional RNDIS Property"
```

## <a name="related-topics"></a>相关主题


[远程 NDIS (RNDIS) 的概述](overview-of-remote-ndis--rndis-.md)

[包含在 Windows 中的 USB 类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

 

 






