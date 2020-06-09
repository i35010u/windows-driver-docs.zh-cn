---
title: usbkd ehci_info_from_fdo
description: Ehci_info_from_fdo usbkd 命令显示有关 USB 主机控制器的信息。
ms.assetid: C7026EF3-F58D-45EB-83D5-8B4A3E661759
keywords:
- usbkd ehci_info_from_fdo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.ehci_info_from_fdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cf9da8b15c2bfbe6c69a88cf526ed2b4f93778c2
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534056"
---
# <a name="usbkdehci_info_from_fdo"></a>！ usbkd \_ \_ fdo 中的信息 \_


[**Fdo 命令中的！ \_ usbkd \_ INFO \_ **](-usbkd-ehci-info-from-fdo.md)显示有关 USB 主机控制器的信息。

```dbgcmd
!usbkd.ehci_info_from_fdo fdo
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______fdo______"></span><span id="_______FDO______"></span>*fdo*   
UHCI 或 EHCI USB 主机控制器的功能设备对象（FDO）的地址。 可以从[**！ usb2tree**](-usbkd-usb2tree.md)命令的输出中获取 FDO 的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd

<a name="examples"></a>示例
--------

首先，使用[**！ usb2tree**](-usbkd-usb2tree.md)命令获取 FDO 的地址。

```dbgcmd
0: kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0

1)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

在上面的输出中，可以看到 USB 主机控制器的 FDO 地址是 `ffffe00001ca1050` 。 将 FDO 的地址传递给[**！ ehci \_ info \_ from \_ FDO**](-usbkd-ehci-info-from-fdo.md)。

```dbgcmd
0: kd> !usbkd.ehci_info_from_fdo ffffe00001ca1050

HC Flavor 1000  FDO ffffe00001ca1050
Root Hub: FDO ffffe00002320050 !hub2_info ffffe000023201a0
Operational Registers ffffd000228bf020
Device Data ffffe00001ca2da0
dt USBPORT!_FDO_EXTENSION ffffe00001ca15a0
DM Timer Flags ffffe00001ca16d4
FDO Flags ffffe00001ca16d0
HCD Log ffffe00001ca11a0

DeviceHandleList: !usblist ffffe00001ca23b8, DL 
DeviceHandleDeletedList: !usblist ffffe00001ca23c8, DL [Empty]
GlobalEndpointList: !usblist ffffe00001ca2388, EP 
EpNeoStateChangeList: !usblist ffffe00001ca2370, SC [Empty]
GlobalTtListHead: !usblist ffffe00001ca23a8, TT [Empty]
BusContextHead: !usblist ffffe00001ca16b0, BC 

## Pending Requests

[001] dt USBPORT!_USB_IOREQUEST_CONTEXT ffffe00001ca1450 Tag: AddD Obj: ffffe00001ca11a0
...

## XDPC List

01) dt USBPORT!_XDPC_CONTEXT ffffe00001ca1f18
...

## PnP FUNC HISTORY (latest at bottom)

[01] IRP_MN_QUERY_CAPABILITIES
...
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线（USB）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






