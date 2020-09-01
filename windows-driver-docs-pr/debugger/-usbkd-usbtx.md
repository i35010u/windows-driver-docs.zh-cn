---
title: usbkd.usbtx
description: Usbkd. usbtx 命令显示 usbport _HCD_TRANSFER_CONTEXT 结构中的信息。
ms.assetid: 603AD207-69D5-4DED-80B5-ADA21E191D47
keywords:
- usbkd usbtx Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbtx
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f3af4e1d26bb40b002b4965f97993af40faaf747
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217929"
---
# <a name="usbkdusbtx"></a>!usbkd.usbtx


**！ Usbkd. usbtx**命令显示 usbport 中的信息 **！ \_HCD \_ 传输 \_ 上下文**结构。

```dbgcmd
!usbkd.usbtx StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbport 的地址 **！ \_HCD \_ 传输 \_ 上下文** 结构。 若要获取 USB 主机控制器的传输列表，请使用 [**！ usbkd. usbhcdext**](-usbkd-usbhcdext.md) 命令。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是查找 usbport 地址的一种方法 **！ \_HCD \_ 传输 \_ 上下文** 结构。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
4)!uhci_info ffffe00001c8f1a0 !devobj ffffe00001c8f050 PCI: VendorId 8086 DeviceId 2938 RevisionId 0002 
...
```

在上面的输出中，FDO 的设备扩展的地址显示为 [DML](debugger-markup-language-commands.md) command **！ uhci \_ info ffffe00001c8f1a0**的参数。

单击 DML 命令或将设备扩展的地址传递给 [**！ usbhcdext**](-usbkd-usbhcdext.md) 以获取传输列表。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001c8f1a0
...
## I/O TRANSFER LIST(s)

1.) Transfer Request Priority List: (TxQueued) Type: 0-NotSplit, 1-Parent, 2-Child
    --------------------------------------------------------------------------------
    [000]!usbtx ffffe0000653401c !usbep ffffe00004730c60 !irp ffffe00004221220 State: (7)TX_Mapped_inMp
        Priority: 0, Type: 0, Flags= 0000000a, SequenceNum: 10, SplitIdx: 0
        InLen: 4096, OutLen: 0 Status: USBD_STATUS_PENDING (0x40000000)
    ...
```

在上面的输出中， `ffffe0000653401c` 是** \_ HCD \_ 传输 \_ 上下文**结构的地址。 将此地址传递给 **！ usbtx**。

```dbgcmd
0: kd> !usbkd.usbtx ffffe0000653401c

dt usbport!_HCD_TRANSFER_CONTEXT ffffe0000653401c
dt usbport!_TRANSFER_PARAMETERS ffffe0000653417c

## TX HISTORY

## EVENT, STATE, NEXT (latest at bottom)

[01]    (23)Ev_TX_Icsq, (0)TX_Undefined, (1)TX_InQueue
[02]    (5)Ev_TX_MapTransfer, (1)TX_InQueue, (2)TX_MapPending
[03]    (7)Ev_TX_MpSubmitSuccess, (2)TX_MapPending, (7)TX_Mapped_inMp

**DMA**
dt usbport!_TRANSFER_SG_LIST ffffe0000653439c
SgCount:  1  MdlVirtualAddress: ffffe00000437000  MdlSystemAddress: ffffe00000437000
    [0] dt usbport!_TRANSFER_SG_ENTRY ffffe000065343bc
    : sysaddr: 0000000000000000 len 0x00001000(4096) offset 0x00000000(0) phys 00000000'ded90000
---
dt usbport!_SCATTER_GATHER_ENTRY ffffe000065343ec
dt _SCATTER_GATHER_LIST ffffe00001bc231c
NumberOfElements = 1
    [0] dt _SCATTER_GATHER_ELEMENT ffffe00001bc232c
     :phys 00000000'ded90000 len 0x00001000(4096)
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

