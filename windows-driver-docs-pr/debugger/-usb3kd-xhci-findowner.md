---
title: usb3kd-xhci_findowner
description: Xhci_findowner usb3kd 命令将查找所有者公用缓冲区。
ms.assetid: 6AA3E41C-5838-4425-B1CE-37A13E8F755E
keywords:
- usb3kd xhci_findowner Windows 调试
ms.date: 10/18/2018
topic_type:
- apiref
api_name:
- usb3kd.xhci_findowner
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f9705fb33ce4f79bd07dee35b1ee5d777db654fc
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534890"
---
# <a name="usb3kdxhci_findowner"></a>！ usb3kd. xhci \_ findowner


**！ Usb3kd. xhci \_ findowner**命令查找所有者公用缓冲区。

```dbgcmd
!usb3kd.xhci_findowner Address
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
公用缓冲区的虚拟或物理地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd

<a name="remarks"></a>备注
-------

公用缓冲区是由硬件寻址的物理上连续的内存块。 USB 3.0 驱动程序堆栈使用公用缓冲区与 USB 3.0 主机控制器进行通信。 假设系统崩溃，而您怀疑可能是常见缓冲区内存的地址。 如果该地址是公用缓冲内存，则此命令将告诉你内存所属的 USB 3.0 主机控制器（如果你有多个 USB 3.0 控制器）以及内存的用途。

<a name="examples"></a>示例
--------

下面的示例调用[**！ xhci \_ resourceusage**](-usb3kd-xhci-resourceusage.md)以列出一些常见缓冲区的地址。

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

前面的输出中列出的某个虚拟地址为0x868e2000。 下面的示例将该地址传递给 **！ xhci \_ findowner**。 前面的输出中列出的其中一个物理地址为0xdb2e4400。 下面的示例将0xdb2e4440 （offset 0x40 bytes from 0xdb2e4400）传递给 **！ xhci \_ findowner**。

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

当你在传输请求块（TRB）中有一个地址，并且想要将该地址跟踪回其所属的设备槽时， **！ xhci \_ findowner**命令特别有用。 在下面的示例中，在[**！ xhci \_ 传输**](-usb3kd-xhci-transferring.md)的输出中列出的一个地址是0xda452230，这是 TRB 的物理地址。 该示例将该地址传递给 **！ xhci \_ findowner**。 输出显示 TRB 属于设备槽8（**！ xhci \_ deviceslots 0x8551d370 8**）。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**！ xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[通用串行总线（USB）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






