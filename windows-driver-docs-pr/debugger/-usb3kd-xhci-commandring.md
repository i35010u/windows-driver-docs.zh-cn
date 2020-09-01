---
title: usb3kd xhci_commandring
description: Xhci_commandring usb3kd 扩展显示与 USB 3.0 主机控制器关联的命令环形数据结构的相关信息。
ms.assetid: 3099F3F1-B881-4BBD-90F5-59DC2DFECF3B
keywords:
- usb3kd xhci_commandring Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_commandring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f97a7cbfc9ca79023d46fe03636540d2967b9346
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206833"
---
# <a name="usb3kdxhci_commandring"></a>！ usb3kd. xhci \_ commandring


[**！ Usb3kd. xhci \_ commandring**](-usb3kd-device-info.md)扩展显示与 USB 3.0 主机控制器关联的命令环形数据结构的相关信息。

```dbgcmd
!usb3kd.xhci_commandring DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*DeviceExtension*   
主机控制器的功能设备对象的设备扩展的 AAddress (FDO) 。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

Output **！ xhci \_ commandring** 命令基于 USB 3.0 主机控制器驱动程序所维护的数据结构 ( # A0) 。 有关 usb 3.0 主机控制器驱动程序和 USB stack 中其他驱动程序的详细信息，请参阅 [Usb 驱动程序堆栈体系结构](../usbcon/usb-3-0-driver-stack-architecture.md)。

命令环是 USB 3.0 主机控制器驱动程序使用的一种数据结构，用于将命令传递给主机控制器。

<a name="examples"></a>示例
--------

若要获取设备扩展的地址，请查看 [**！ xhci \_ dumpall**](-usb3kd-xhci-dumpall.md) 命令的输出。 在以下示例中，设备扩展的地址为0xfffffa800536e2d0。

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

现在可以将设备扩展的地址传递给 **！ xhci \_ commandring** 命令。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**！ xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

