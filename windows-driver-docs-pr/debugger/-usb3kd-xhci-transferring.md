---
title: usb3kd.xhci_transferring
description: Usb3kd.xhci_transferring 扩展显示 USB 3.0 主机) 控制器 (使用的传输环，直到它检测到循环位更改。
keywords:
- usb3kd.xhci_transferring Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_transferring
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c4a5731429d1fbdd5033b8c2de468e5052bdbe14
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838409"
---
# <a name="usb3kdxhci_transferring"></a>！ usb3kd xhci 正在 \_ 传输


[**！ Usb3kd \_ 传输**](-usb3kd-device-info.md)扩展显示 USB 3.0 主机控制器) 使用的传输 (环，直到它检测到循环位更改。

```dbgcmd
!usb3kd.xhci_transferring VirtualAddress
!usb3kd.xhci_transferring PhysicalAddress 1
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span>*VirtualAddress*   
传输环状的虚拟地址。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span>*PhysicalAddress*   
传输环状的物理地址。

<span id="_______1______"></span> 2   
指定该地址是一个物理地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

**！ Xhci \_ 传输** 命令的输出基于 USB 3.0 主机控制器驱动程序所维护的数据结构 ( # A0) 。 有关 usb 3.0 主机控制器驱动程序和 USB 堆栈中其他驱动程序的详细信息，请参阅 [Windows 中的 usb 主机端驱动程序](../usbcon/usb-3-0-driver-stack-architecture.md)。

传输环是 USB 3.0 主机控制器驱动程序使用的结构，用于维护传输请求块 (TRBs) 的列表。 此命令获取传输环的虚拟或物理地址，但显示 TRBs 的物理地址。 这样做是为了使命令能够正确遍历链接 TRBs。

<a name="examples"></a>示例
--------

若要获取传输环的地址，请查看 [**！ xhci \_ deviceslots**](-usb3kd-xhci-deviceslots.md) 命令的输出。 在下面的示例中，传输环的虚拟地址为0xfffffa8005b2fe00。

```dbgcmd
3: kd> !usb3kd.xhci_deviceslots 0xfffffa800523a2d0

## Dumping dt _DEVICESLOT_DATA 0xfffffa80051a3300
----------------------------------------------
DeviceContextBase: VA 0xfffffa8005a41000 LA 0x116841000 !wdfcommonbuffer 0x57ffa6ff9b8 Size 4096

## [1] SlotID : dt USBXHCI!_USBDEVICE_DATA 0xfffffa800598c7d0 dt _SLOT_CONTEXT32 0xfffffa8005a42000
------------------------------------------------------------------------------------------------
    USB\VID_125F&PID_312A ADATA Technology Co., Ltd.
    SlotEnabled IsDevice NumberOfTTs 0 TTThinkTime 0
    Speed: Super PortPathDepth: 1 PortPath: [ 2 ] DeviceAddress: 1
    !device_info_from_pdo 0xfffffa800597d720
    DeviceContextBuffer: VA 0xfffffa8005a42000 LA 0x116842000 !wdfcommonbuffer 0x57ffa7009b8 Size 4096
    InputDeviceContextBuffer: VA 0xfffffa8005b2d000 LA 0x11692d000 !wdfcommonbuffer 0x57ffa674958 Size 4096
    ...

    [3] DeviceContextIndex : dt USBXHCI!_ENDPOINT_DATA 0xfffffa8005b394e0 dt _ENDPOINT_CONTEXT32 0xfffffa8005a42060 ES_RUNNING
    --------------------------------------------------------------------------------------------------------------
       ...
            CurrentRingBufferData: VA 0xfffffa8005b2fe00 LA 0x11692fe00 !wdfcommonbuffer 0x57ffa67c988 Size 512
            Current:  !xhci_transferring 0xfffffa8005b2fe00
            PendingTransferList: 
                [0] dt _TRANSFER_DATA 0xfffffa8005b961b0 !urb 0xfffffa8005b52be8 !wdfrequest 0x57ffa469fd8 TransferState_Pending
```

现在可以将传输环的地址传递到 **！ xhci \_ 传输** 命令。

```dbgcmd
kd> !xhci_transferring 0xfffffa8005b2fe00

        [  0] NORMAL       0x000000011692fe00 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 0 TransferLength    13 TDSize  0
        [  1] EVENT_DATA   0x000000011692fe10 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 0 Data  0 0xfffffa8005986850 TotalBytes 13
        [  2] NORMAL       0x000000011692fe20 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 0 TransferLength    13 TDSize  0
        [  3] EVENT_DATA   0x000000011692fe30 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 0 Data  0 0xfffffa8005b96210 TotalBytes 13
        [  4] NORMAL       0x000000011692fe40 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 0 TransferLength    13 TDSize  0
        [  5] EVENT_DATA   0x000000011692fe50 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 0 Data  0 0xfffffa8005b96210 TotalBytes 13
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**！ xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

