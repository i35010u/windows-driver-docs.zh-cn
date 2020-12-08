---
title: usb3kd.xhci_eventring
description: Usb3kd.xhci_eventring 扩展显示与 USB 3.0 主机控制器关联的事件环数据结构的相关信息。
keywords:
- usb3kd.xhci_eventring Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_eventring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 92676078c836e75be77e85d3752212762d8311a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839031"
---
# <a name="usb3kdxhci_eventring"></a>！ usb3kd. xhci \_ eventring


[**！ Usb3kd. xhci \_ eventring**](-usb3kd-device-info.md)扩展显示与 USB 3.0 主机控制器关联的事件环数据结构的相关信息。

```dbgcmd
!usb3kd.xhci_eventring DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*DeviceExtension*   
主机控制器的功能设备对象的设备扩展的地址 (FDO) 。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

Output **！ xhci \_ eventring** 命令基于 USB 3.0 主机控制器驱动程序所维护的数据结构 ( # A0) 。 有关 usb 3.0 主机控制器驱动程序和 USB 堆栈中其他驱动程序的详细信息，请参阅 [Windows 中的 usb 主机端驱动程序](../usbcon/usb-3-0-driver-stack-architecture.md)。

事件环是 USB 3.0 主机控制器用于通知驱动程序操作已完成的结构。

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
    !xhci_deviceslots 0xfffffa800536e2d0
    !xhci_eventring 0xfffffa800536e2d0
    ...
```

现在可以将设备扩展的地址传递给 **！ xhci \_ eventring** 命令。

```dbgcmd
3: kd> !xhci_eventring 0xfffffa800536e2d0

## Dumping dt _PRIMARY_INTERRUPTER_DATA fffffa800536b5b0
-----------------------------------------------------

## [0] Interrupter : dt _INTERRUPTER_DATA 0xfffffa800536b7d0  !rcdrlogdump USBXHCI -a 0xfffffa8005aeab60
------------------------------------------------------------------------------------------------------
    DequeueSegment: 1 DequeueIndex: 217 TotalEventRingSegments: 2 TRBsPerSegment: 256
    CurrentBufferData : VA 0xfffffa8005373000 LA 0x117173000 !wdfcommonbuffer 0x57ffa65b9b8 Size 4096
    EventRingTableBufferData : VA 0xfffffa8005aeb000 LA 0x1168eb000 !wdfcommonbuffer 0x57ffa65d988 Size 512

    [0] VA 0xfffffa8005370000 LA 0x117170000 !wdfcommonbuffer 0x57ffa6599b8 Size 4096
    [1] VA 0xfffffa8005373000 LA 0x117173000 !wdfcommonbuffer 0x57ffa65b9b8 Size 4096

    Event Ring TRBs:
        [207] TRANSFER_EVENT      0xfffffa8005373cf0 CycleBit 0 SlotId  2 EndpointID  4 EventData 1 Pointer 0xfffffa8005366700 CC_SUCCESS
        [208] TRANSFER_EVENT      0xfffffa8005373d00 CycleBit 0 SlotId  2 EndpointID  3 EventData 1 Pointer 0xfffffa8005a3d850 CC_SHORT_PACKET
        [209] TRANSFER_EVENT      0xfffffa8005373d10 CycleBit 0 SlotId  1 EndpointID  4 EventData 1 Pointer 0xfffffa8005a3d850 CC_SUCCESS
        [210] TRANSFER_EVENT      0xfffffa8005373d20 CycleBit 0 SlotId  1 EndpointID  3 EventData 1 Pointer 0xfffffa8005366700 CC_SUCCESS
        [211] TRANSFER_EVENT      0xfffffa8005373d30 CycleBit 0 SlotId  2 EndpointID  4 EventData 1 Pointer 0xfffffa8005366700 CC_SUCCESS
        [212] TRANSFER_EVENT      0xfffffa8005373d40 CycleBit 0 SlotId  2 EndpointID  3 EventData 1 Pointer 0xfffffa8005a3d850 CC_SHORT_PACKET
        [213] TRANSFER_EVENT      0xfffffa8005373d50 CycleBit 0 SlotId  1 EndpointID  4 EventData 1 Pointer 0xfffffa8005a3d850 CC_SUCCESS
        [214] TRANSFER_EVENT      0xfffffa8005373d60 CycleBit 0 SlotId  1 EndpointID  3 EventData 1 Pointer 0xfffffa8005366700 CC_SUCCESS
        [215] TRANSFER_EVENT      0xfffffa8005373d70 CycleBit 0 SlotId  2 EndpointID  4 EventData 1 Pointer 0xfffffa8005366700 CC_SUCCESS
        [216] TRANSFER_EVENT      0xfffffa8005373d80 CycleBit 0 SlotId  2 EndpointID  3 EventData 1 Pointer 0xfffffa8005a3d850 CC_SHORT_PACKET
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**！ xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

