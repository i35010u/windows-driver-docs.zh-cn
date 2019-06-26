---
title: usbkd.usbhcdlist
description: Usbkd.usbhcdlist 命令显示有关 USB 端口驱动程序 (Usbport.sys) 表示的所有 USB 主控制器的信息。
ms.assetid: 877A6361-0DB9-4089-AF85-BABFBED8C440
keywords:
- usbkd.usbhcdlist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdlist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e0557c1a730c30e416d11f9b861a583bfce97b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362439"
---
# <a name="usbkdusbhcdlist"></a>!usbkd.usbhcdlist


[ **！ Usbkd.usbhcdlist** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-usbkd-usbhcdlist)命令显示有关 USB 端口驱动程序 (Usbport.sys) 表示的所有 USB 主控制器的信息。 有关 USB 端口驱动程序和关联的微型端口驱动程序的信息，请参阅[USB 驱动程序堆栈体系结构](https://go.microsoft.com/fwlink/p?LinkId=251983)。

```dbgcmd
!usbkd.usbhcdlist
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是示例的输出的一部分[ **！ usbhcdlist**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-usbkd-usbhcdlist)。

```dbgcmd
0: kd> !usbkd.usbhcdlist
MINIPORT List @ fffff80001e5bbd0

## List of UHCI controllers

!drvobj ffffe00002000060 dt USBPORT!_USBPORT_MINIPORT_DRIVER ffffe00001f48010 Registration Packet ffffe00001f48048

01
...

## List of EHCI controllers

!drvobj ffffe00001fd33a0 dt USBPORT!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0 Registration Packet ffffe00001f48c08

01. Xxxxx Corporation PCI: VendorID Xxxx DeviceID Xxxx RevisionId 0002
    !devobj ffffe00001ca1050
    !ehci_info ffffe00001ca11a0
    Operational Registers ffffd000228bf020
    Device Data ffffe00001ca2da0
    !usbhcdlog ffffe00001ca11a0
    nt!_KINTERRUPT ffffe000020abe78
    Device Capabilities ffffe00001ca135c
    Pending IRP's: 0, Transfers: 0 (Periodic(0), Async(0))
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






