---
title: usb3kd.xhci_trb
description: 'Usb3kd.xhci_trb 扩展显示 USB 3.0 主机控制器使用的一个或多个传输请求块 (TRBs) '
keywords:
- usb3kd.xhci_trb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_trb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 077f40e3a1d186b2c8941573cb94f3b2e7b0f19f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817001"
---
# <a name="usb3kdxhci_trb"></a>！ usb3kd. xhci \_ trb


[**！ Usb3kd. xhci \_ trb**](-usb3kd-device-info.md)扩展显示 USB 3.0 主机控制器使用的一个或多个传输请求块 (TRBs) 

```dbgcmd
!usb3kd.xhci_trb VirtualAddress Count
!usb3kd.xhci_trb PhysicalAddress Count 1
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span>*VirtualAddress*   
TRB 的虚拟地址。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span>*PhysicalAddress*   
TRB 的物理地址。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span>*计数*   
要显示的连续 TRBs 数，从 *VirtualAddress* 或 *PhysicalAddress* 开始。

<span id="_______1______"></span> 2   
指定该地址是一个物理地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

Output [**！ xhci \_ trb**](-usb3kd-device-info.md) 命令基于 USB 3.0 主机控制器驱动程序所维护的数据结构 ( # A0) 。 有关 usb 3.0 主机控制器驱动程序和 USB 堆栈中其他驱动程序的详细信息，请参阅 [Windows 中的 usb 主机端驱动程序](../usbcon/usb-3-0-driver-stack-architecture.md)。

<a name="examples"></a>示例
--------

在下面的示例中， **0x844d7c00** 是 TRB 的虚拟地址。 **1** 是计数，它指定要显示的连续 TRBs 的数目。

```dbgcmd
0: kd> !xhci_trb 0x844d7c00 1

        [  0] ISOCH        0x844d7c00 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  2688 TDSize  0 TBC 0 TLBPC 2 Frame 0x3D2
```

在下面的示例中， **0x0dced7c00** 是 TRB 的物理地址。 **4** 是计数，它指定要显示的连续 TRBs 的数目。 **1** 指定地址为物理地址。

```dbgcmd
0: kd> !xhci_trb 0x0dced7c00 4 1

        [  0] ISOCH        0xdced7c00 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  2688 TDSize  0 TBC 0 TLBPC 2 Frame 0x3D2
        [  1] EVENT_DATA   0xdced7c10 CycleBit 1 IOC 1 CH 0 BEI 1 InterrupterTarget 1 Data 0x194c9bcf001b0001 PacketId 27 Frame 0x194c9bcf TotalBytes 2688
        [  2] ISOCH        0xdced7c20 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  1352 TDSize  2 TBC 0 TLBPC 2 Frame 0x3D2
        [  3] NORMAL       0xdced7c30 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  1336 TDSize  0
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**！ xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

