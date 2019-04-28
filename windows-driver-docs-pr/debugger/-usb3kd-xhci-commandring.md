---
title: usb3kd.xhci_commandring
description: Usb3kd.xhci_commandring 扩展显示有关与 USB 3.0 主机控制器相关联的命令环数据结构的信息。
ms.assetid: 3099F3F1-B881-4BBD-90F5-59DC2DFECF3B
keywords:
- usb3kd.xhci_commandring Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_commandring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 16afbd844b7a29c2b15db887ca83a44110c92411
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330769"
---
# <a name="usb3kdxhcicommandring"></a>!usb3kd.xhci\_commandring


[ **！ Usb3kd.xhci\_commandring** ](-usb3kd-device-info.md)扩展显示有关与 USB 3.0 主机控制器相关联的命令环数据结构的信息。

```dbgcmd
!usb3kd.xhci_commandring DeviceExtension
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
适用于主机控制器的功能的设备对象 (FDO) 的设备扩展 AAddress。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

输出 **！ xhci\_commandring**命令基于 USB 3.0 主机控制器驱动程序 (UsbXhci.sys) 维护的数据结构。 有关 USB 3.0 主机控制器驱动程序和 USB 堆栈中的其他驱动程序的详细信息，请参阅[USB 驱动程序堆栈体系结构](https://go.microsoft.com/fwlink/p?LinkID=251983)。

命令环是一个 USB 3.0 主机控制器驱动程序用于将命令传递到主控制器的数据结构。

<a name="examples"></a>示例
--------

若要获取设备扩展的地址，请查看的输出[ **！ xhci\_dumpall** ](-usb3kd-xhci-dumpall.md)命令。 在以下示例中，设备扩展的地址是 0xfffffa800536e2d0。

```dbgcmd
3: kd> !xhci_dumpall

## Dumping all the XHCI controllers - DrvObj 0xfffffa80053072f0
------------------------------------------------------------
1)  ... - PCI: VendorId ... DeviceId ... RevisionId ... Firmware ...

    dt USBXHCI!_CONTROLLER_DATA 0xfffffa80052f20c0
    !rcdrlogdump USBXHCI -a 0xfffffa8005068520
    !rcdrlogdump USBXHCI -a 0xfffffa8004e8b9a0 (rundown)
    !wdfdevice 0x57ffac91fd8
    !xhci_capability 0xfffffa800536e2d0
    !xhci_registers 0xfffffa800536e2d0
    !xhci_commandring 0xfffffa800536e2d0 (No commands are pending)
    ...
```

现在可以将传递到设备扩展的地址 **！ xhci\_commandring**命令。

```dbgcmd
3: kd> !xhci_commandring 0xfffffa800536e2d0

## Dumping dt _COMMAND_DATA 0xfffffa8005362f70 !rcdrlogdump USBXHCI -a 0xfffffa8005a8f010
-------------------------------------------------------------------------------------
Stop: OFF Abort: OFF Running: ON
CommandRingBufferData: VA 0xfffffa8005aeb200 LA 0x1168eb200 !wdfcommonbuffer 0x57ffa65d988 Size 512
DequeueIndex: 24 EnqueueIndex: 24 CycleState: 0

    Command Ring TRBs:
        [  0] Unknown TRB Type 49 0xfffffa8005aeb200

        [  1] ENABLE_SLOT                 0xfffffa8005aeb210 CycleBit 1
        [  2] ADDRESS_DEVICE              0xfffffa8005aeb220 CycleBit 1 SlotId  1 BlockSetAddressRequest 1
        ...

    PendingList:
        Empty List

    WaitingList:
        Empty List
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**!xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






