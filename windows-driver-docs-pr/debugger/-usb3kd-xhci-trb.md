---
title: usb3kd.xhci_trb
description: Usb3kd.xhci_trb 扩展插件都会显示一个或多个传输请求 (TRBs) 所使用的块的 USB 3.0 主控制器
ms.assetid: 6EC90908-320E-4908-BE53-1AD01A81B140
keywords:
- usb3kd.xhci_trb Windows Debugging
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.xhci_trb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4a3a39bb133dc3827b3dc0b94421669c05e9ab2a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335628"
---
# <a name="usb3kdxhcitrb"></a>!usb3kd.xhci\_trb


[ **！ Usb3kd.xhci\_trb** ](-usb3kd-device-info.md)扩展插件都会显示一个或多个传输请求 (TRBs) 所使用的块的 USB 3.0 主控制器

```dbgcmd
!usb3kd.xhci_trb VirtualAddress Count
!usb3kd.xhci_trb PhysicalAddress Count 1
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span> *VirtualAddress*   
TRB 虚拟地址。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span> *PhysicalAddress*   
TRB 物理地址。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *Count*   
连续 TRBs 若要显示，数开始*VirtualAddress*或*PhysicalAddress*。

<span id="_______1______"></span> 1   
指定的地址是一个物理地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

输出[ **！ xhci\_trb** ](-usb3kd-device-info.md)命令基于 USB 3.0 主机控制器驱动程序 (UsbXhci.sys) 维护的数据结构。 有关 USB 3.0 主机控制器驱动程序和 USB 堆栈中的其他驱动程序的详细信息，请参阅[USB 驱动程序堆栈体系结构](https://go.microsoft.com/fwlink/p?LinkID=251983)。

<a name="examples"></a>示例
--------

在以下示例中， **0x844d7c00**是 TRB 的虚拟地址。 **1**是计数，它指定数量的连续 TRBs 显示。

```dbgcmd
0: kd> !xhci_trb 0x844d7c00 1

        [  0] ISOCH        0x844d7c00 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  2688 TDSize  0 TBC 0 TLBPC 2 Frame 0x3D2
```

在以下示例中， **0x0dced7c00**是 TRB 的物理地址。 **4**是计数，它指定数量的连续 TRBs 显示。 **1**指定的地址是一个物理地址。

```dbgcmd
0: kd> !xhci_trb 0x0dced7c00 4 1

        [  0] ISOCH        0xdced7c00 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  2688 TDSize  0 TBC 0 TLBPC 2 Frame 0x3D2
        [  1] EVENT_DATA   0xdced7c10 CycleBit 1 IOC 1 CH 0 BEI 1 InterrupterTarget 1 Data 0x194c9bcf001b0001 PacketId 27 Frame 0x194c9bcf TotalBytes 2688
        [  2] ISOCH        0xdced7c20 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  1352 TDSize  2 TBC 0 TLBPC 2 Frame 0x3D2
        [  3] NORMAL       0xdced7c30 CycleBit 1 IOC 0 CH 1 BEI 0 InterrupterTarget 1 TransferLength  1336 TDSize  0
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[**!xhci\_dumpall**](-usb3kd-xhci-dumpall.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






