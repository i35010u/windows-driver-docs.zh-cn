---
title: usbkd.usbhcdlist
description: Usbkd. usbhcdlist 命令显示有关 USB 端口驱动程序（Usbport）表示的所有 USB 主机控制器的信息。
ms.assetid: 877A6361-0DB9-4089-AF85-BABFBED8C440
keywords:
- usbkd usbhcdlist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdlist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0386e8e89780cd874a507cfa87e7256f29d518b8
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534696"
---
# <a name="usbkdusbhcdlist"></a>!usbkd.usbhcdlist


[**！ Usbkd. usbhcdlist**](-usbkd-usbhcdlist.md)命令显示有关 usb 端口驱动程序（Usbport）表示的所有 usb 主机控制器的信息。 有关 USB 端口驱动程序和关联的微型端口驱动程序的信息，请参阅[Windows 中的 usb 主机端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)。

```dbgcmd
!usbkd.usbhcdlist
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd

<a name="examples"></a>示例
--------

下面是[**！ usbhcdlist**](-usbkd-usbhcdlist.md)的输出部分的示例。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线（USB）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






