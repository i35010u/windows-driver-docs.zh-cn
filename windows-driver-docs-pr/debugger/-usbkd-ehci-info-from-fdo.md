---
title: usbkd.ehci_info_from_fdo
description: Usbkd.ehci_info_from_fdo 命令显示有关 USB 主控制器的信息。
ms.assetid: C7026EF3-F58D-45EB-83D5-8B4A3E661759
keywords:
- usbkd.ehci_info_from_fdo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.ehci_info_from_fdo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c13ea095d4d30e19b43dc91df331665a656130ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334116"
---
# <a name="usbkdehciinfofromfdo"></a>!usbkd.ehci\_info\_from\_fdo


[ **！ Usbkd.ehci\_信息\_从\_fdo** ](https://msdn.microsoft.com/library/windows/hardware/dn367058)命令显示有关 USB 主控制器的信息。

```dbgcmd
!usbkd.ehci_info_from_fdo fdo
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______fdo______"></span><span id="_______FDO______"></span> *fdo*   
UHCI 或 EHCI USB 主控制器的功能的设备对象 (FDO) 的地址。 可以从的输出中获取的地址 FDO [ **！ usb2tree** ](-usbkd-usb2tree.md)命令。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

首先，使用[ **！ usb2tree** ](-usbkd-usb2tree.md)命令来获取 FDO 的地址。

```dbgcmd
0: kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0

1)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

在上面的输出，您可以看到的 USB 主控制器 FDO 的地址是`ffffe00001ca1050`。 传递到 FDO 的地址[ **！ ehci\_信息\_从\_fdo**](https://msdn.microsoft.com/library/windows/hardware/dn367058)。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






