---
title: usb3kd-xhci_findowner
description: Usb3kd.xhci_findowner 命令查找所有者常见缓冲区。
ms.assetid: 6AA3E41C-5838-4425-B1CE-37A13E8F755E
keywords:
- usb3kd.xhci_findowner Windows 调试
ms.date: 10/18/2018
topic_type:
- apiref
api_name:
- usb3kd.xhci_findowner
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed0c94f1e05aa891a77ba29406af2d84c4adbef1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330779"
---
# <a name="usb3kdxhcifindowner"></a>!usb3kd.xhci\_findowner


**！ Usb3kd.xhci\_findowner**命令查找所有者常见缓冲区。

```dbgcmd
!usb3kd.xhci_findowner Address
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
常见的缓冲区的虚拟或物理地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

一个常见缓冲区就是进行寻址的硬件的物理上连续内存块。 USB 3.0 驱动程序堆栈使用常见的缓冲区的 USB 3.0 主机控制器进行通信。 假设系统崩溃，并会遇到您怀疑可能是常见的缓冲区内存的地址。 如果地址是常见的缓冲区内存，此命令会告诉你哪些 USB 3.0 主机控制器所属的内存 （在本例中您有多个 USB 3.0 控制器） 和内存都用尽。

<a name="examples"></a>示例
--------

下面的示例调用[ **！ xhci\_resourceusage** ](-usb3kd-xhci-resourceusage.md)列出一些常见的缓冲区的地址。

```dbgcmd
0: kd> !usb3kd.xhci_resourceusage 0x867fbff0

## Dumping CommonBuffer Resources
------------------------------
    dt USBXHCI!_COMMON_BUFFER_DATA 0x868d61c0
    DmaEnabler:!wdfdmaenabler 0x79729fe8

    CommonBuffers Large: Total 8 Available 2 Used 6 TotalBytes 32768
        [ 1] dt _TRACKING_DATA 0x868d73a4 VA 0x868e0000 LA 0xdb2e0000 -- Owner 0x86801690 Tag: Int2 Size 4096
        [ 2] dt _TRACKING_DATA 0x868d6d1c VA 0x868e1000 LA 0xdb2e1000 -- Owner 0x86801690 Tag: Int2 Size 4096
        [ 3] dt _TRACKING_DATA 0x868d6c54 VA 0x868e2000 LA 0xdb2e2000 -- Owner 0x86801690 Tag: Int2 Size 4096
        [ 4] dt _TRACKING_DATA 0x868d6b8c VA 0x868e3000 LA 0xdb2e3000 -- Owner 0x86801690 Tag: Int2 Size 4096
        [ 5] dt _TRACKING_DATA 0x868d67b4 VA 0x868e5000 LA 0xdb2e5000 -- Owner 0x86801548 Tag: Slt1 Size 4096
        [ 6] dt _TRACKING_DATA 0x868d50b4 VA 0x868e6000 LA 0xdb2e6000 -- Owner 0x86801548 Tag: Slt3 Size 4096

    CommonBuffers Small: Total 16 Available 13 Used 3 TotalBytes 8192
        [ 1] dt _TRACKING_DATA 0x868d6974 VA 0x868e4000 LA 0xdb2e4000 -- Owner 0x86801690 Tag: Int1 Size 512
        [ 2] dt _TRACKING_DATA 0x868d69a4 VA 0x868e4200 LA 0xdb2e4200 -- Owner 0x86801548 Tag: Slt2 Size 512
        [ 3] dt _TRACKING_DATA 0x868d69d4 VA 0x868e4400 LA 0xdb2e4400 -- Owner 0x86801488 Tag: Cmd1 Size 512
```

上面的输出中列出的虚拟地址之一是 0x868e2000。 下面的示例将传递到该地址 **！ xhci\_findowner**。 上面的输出中列出的物理地址之一是 0xdb2e4400。 下面的示例将 0xdb2e4440 （0xdb2e4400 从偏移量 0x40 字节） 传递给 **！ xhci\_findowner**。

```dbgcmd
0: kd> !xhci_findowner 0x868e2000 

!xhci_info 0x867fbff0  Texas Instruments - PCI: VendorId 0x104c DeviceId 0x8241 RevisionId 0x02

    dt _TRACKING_DATA 0x868d6c54 VA 0x868e2000 LA 0xdb2e2000 -- Owner 0x86801690 Tag: Int2 Size 4096

    dt _INTERRUPTER_DATA 0x86801690 
    !xhci_eventring 0x867fbff0  <-- This memory is used for event ring.


0: kd> !xhci_findowner 0xdb2e4440  <-- Note the offset difference.

!xhci_info 0x867fbff0  Texas Instruments - PCI: VendorId 0x104c DeviceId 0x8241 RevisionId 0x02

    dt _TRACKING_DATA 0x868d69d4 VA 0x868e4400 LA 0xdb2e4400 -- Owner 0x86801488 Tag: Cmd1 Size 512

    dt _COMMAND_DATA 0x86801488 
    !xhci_commandring 0x867fbff0  <-- This memory is used for command ring.
```

**！ Xhci\_findowner**命令在传输请求块 (TRB) 中有一个地址，并且你想要跟踪回其所属的设备槽时尤其有用。 在以下示例中，一个地址的输出中列出[ **！ xhci\_传输**](-usb3kd-xhci-transferring.md)是 0xda452230，这是 TRB 的物理地址。 该示例将传递到该地址 **！ xhci\_findowner**。 该输出显示 TRB 属于设备插槽 8 (**！ xhci\_deviceslots 0x8551d370 8**)。

```dbgcmd
0: kd> !usb3kd.xhci_transferring 0x87652200

        [  0] NORMAL       0xda452200 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 2 TransferLength     6 TDSize  0
        [  1] EVENT_DATA   0xda452210 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 2 Data 0x8511375c TotalBytes 6
        [  2] NORMAL       0xda452220 CycleBit 1 IOC 0 BEI 0 InterrupterTarget 2 TransferLength     6 TDSize  0
        [  3] EVENT_DATA   0xda452230 CycleBit 1 IOC 1 BEI 0 InterrupterTarget 2 Data 0x857d076c TotalBytes 6

0: kd> !xhci_findowner 0xda452230 

!xhci_info 0x8551d370  Renesas - PCI: VendorId 0x1912 DeviceId 0x0015 RevisionId 0x02 Firmware 0x0020.0006

    dt _TRACKING_DATA 0x8585fd5c VA 0x87652200 LA 0xda452200 -- Owner 0x85894548 Tag: Rng1 Size 512

    !xhci_deviceslots 0x8551d370 8

    [0] dt _TRANSFERRING_DATA 0x85894548 Events: 0x0 TransferRingState_Idle
    ------------------------------------------------------------------------------
        WdfQueue: !wdfqueue 0x7a76bcb0 (0 waiting)
        CurrentRingBufferData: VA 0x87652200 LA 0xda452200 !wdfcommonbuffer 0x7a7a0370 Size 512
        Current:  !xhci_transferring 0x87652200
        PendingTransferList: 
            [0] dt _TRANSFER_DATA 0x851136f0 !urb 0x84e55468 !wdfrequest 0x7aeec9e8 TransferState_Pending
            [1] dt _TRANSFER_DATA 0x857d0700 !urb 0x85733be8 !wdfrequest 0x7a82f9d8 TransferState_Pending
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**!xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






