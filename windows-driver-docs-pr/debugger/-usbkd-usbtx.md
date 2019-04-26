---
title: usbkd.usbtx
description: Usbkd.usbtx 命令显示 usbport _HCD_TRANSFER_CONTEXT 结构中的信息。
ms.assetid: 603AD207-69D5-4DED-80B5-ADA21E191D47
keywords:
- usbkd.usbtx Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbtx
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aa91dd9e40441df750420fd6deb7b11713f6bf80
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327975"
---
# <a name="usbkdusbtx"></a>!usbkd.usbtx


**！ Usbkd.usbtx**命令显示中的信息**usbport ！\_HCD\_传输\_上下文**结构。

```dbgcmd
!usbkd.usbtx StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
地址**usbport ！\_HCD\_传输\_上下文**结构。 若要获取传输列表为 USB 主控制器，请使用[ **！ usbkd.usbhcdext** ](-usbkd-usbhcdext.md)命令。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种方法，若要查找的地址**usbport ！\_HCD\_传输\_上下文**结构。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
4)!uhci_info ffffe00001c8f1a0 !devobj ffffe00001c8f050 PCI: VendorId 8086 DeviceId 2938 RevisionId 0002 
...
```

在上面的输出，FDO 设备扩展的地址显示为的参数[DML](debugger-markup-language-commands.md)命令 **！ uhci\_信息 ffffe00001c8f1a0**。

单击 DML 命令或传递到设备扩展的地址[ **！ usbhcdext** ](https://msdn.microsoft.com/library/windows/hardware/dn367072)获取传输列表。

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

在上面的输出`ffffe0000653401c`是地址 **\_HCD\_传输\_上下文**结构。 传递到此地址 **！ usbtx**。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






