---
title: usbkd.usbep
description: Usbkd.usbep 命令显示有关 USB 终结点的信息。
ms.assetid: FEF66394-0502-4F3F-ACBE-57AA1945CC74
keywords:
- usbkd.usbep Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbep
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 38d6386e8e70e06e84aab1d54f174b1313792b94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334107"
---
# <a name="usbkdusbep"></a>!usbkd.usbep


**！ Usbkd.usbep**命令显示有关 USB 终结点的信息。

```dbgcmd
!usbkd.usbep StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
地址**usbport ！\_HCD\_终结点**结构。 若要获得 USB 主控制器的终结点列表，请使用[ **！ usbkd.usbhcdext** ](-usbkd-usbhcdext.md)命令。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种方法，若要查找的地址**usbport ！\_HCD\_终结点**结构。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
     ...
```

在上面的输出，FDO 设备扩展的地址显示为的参数[DML](debugger-markup-language-commands.md)命令 **！ ehci\_信息 ffffe00001ca11a0**。

单击 DML 命令或传递到设备扩展的地址[ **！ usbhcdext** ](https://msdn.microsoft.com/library/windows/hardware/dn367072)获取全局终结点列表。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001ca11a0
...
DeviceHandleList: !usblist ffffe00001ca23b8, DL 
DeviceHandleDeletedList: !usblist ffffe00001ca23c8, DL [Empty]
GlobalEndpointList: !usblist ffffe00001ca2388, EP 
...
```

现在，使用[ **！ usbkd.usblist** ](-usbkd-usblist.md)命令来获取的地址 **\_HCD\_终结点**结构。

```dbgcmd
0: kd> !usblist ffffe00001ca2388, EP

list: ffffe00001ca2388 EP
----------
dt usbport!_HCD_ENDPOINT ffffe000020f6970  !usbep ffffe000020f6970
Device Address: 0x00, ep 0x00 Control  Flags: 00000002 dt _USB_ENDPOINT_FLAGS ffffe000020f6990
dt usbport!_ENDPOINT_PARAMETERS ffffe000020f6b18    RootHub Endpoint
...
```

在上面的输出`ffffe000020f6970 `是地址 **\_HCD\_终结点**结构。 传递到此地址 **！ usbkd.usbep**。

```dbgcmd
0: kd> !usbep ffffe000020f6970
Device Address: 0x00, Endpoint Address 0x00 Endpoint Type: Control 
dt USBPORT!_HCD_ENDPOINT ffffe000020f6970
dt USBPORT!_ENDPOINT_PARAMETERS ffffe000020f6b18
RootHub Endpoint

## Transfer(s) List: (HwPendingListHead)

    [EMPTY]

## Endpoint Reference List: (EpRefListHead)

[00] dt USBPORT!_USBOBJ_REF ffffe000021a64a0 Object ffffe000020f6970 Tag:EPop Endpoint:ffffe000020f6970
[01] dt USBPORT!_USBOBJ_REF ffffe000021264a0 Object ffffe000020f95e0 Tag:EPpi Endpoint:ffffe000020f6970

## GEP HISTORY (latest at bottom)

##      EVENT                   STATE                     NEXT                      HwEpState

[01] Ev_gEp_Open             GEp_Init                  GEp_Paused                ENDPOINT_PAUSE
[02] Ev_gEp_ReqActive        GEp_Paused                GEp_Active                ENDPOINT_ACTIVE
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






