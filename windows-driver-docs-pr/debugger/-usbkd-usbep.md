---
title: usbkd.usbep
description: Usbkd. usbep 命令显示有关 USB 终结点的信息。
keywords:
- usbkd usbep Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbep
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8c2af64f33c171142fac15f5bb725c36d3b000b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818717"
---
# <a name="usbkdusbep"></a>!usbkd.usbep


**！ Usbkd. usbep** 命令显示有关 USB 终结点的信息。

```dbgcmd
!usbkd.usbep StructAddr
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbport 的地址 **！ \_HCD \_ 终结点** 结构。 若要获取 USB 主机控制器的终结点列表，请使用 [**！ usbkd. usbhcdext**](-usbkd-usbhcdext.md) 命令。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是查找 usbport 地址的一种方法 **！ \_HCD \_ 终结点** 结构。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
     ...
```

在上面的输出中，FDO 的设备扩展的地址显示为 [DML](debugger-markup-language-commands.md) 命令 **！ ehci \_ info ffffe00001ca11a0** 的参数。

单击 DML 命令或将设备扩展的地址传递给 [**！ usbhcdext**](-usbkd-usbhcdext.md) 以获取全局终结点列表。

```dbgcmd
0: kd> !usbkd.usbhcdext ffffe00001ca11a0
...
DeviceHandleList: !usblist ffffe00001ca23b8, DL 
DeviceHandleDeletedList: !usblist ffffe00001ca23c8, DL [Empty]
GlobalEndpointList: !usblist ffffe00001ca2388, EP 
...
```

现在使用 [**！ usbkd. usblist**](-usbkd-usblist.md)命令获取 **\_ HCD \_ 终结点** 结构的地址。

```dbgcmd
0: kd> !usblist ffffe00001ca2388, EP

list: ffffe00001ca2388 EP
----------
dt usbport!_HCD_ENDPOINT ffffe000020f6970  !usbep ffffe000020f6970
Device Address: 0x00, ep 0x00 Control  Flags: 00000002 dt _USB_ENDPOINT_FLAGS ffffe000020f6990
dt usbport!_ENDPOINT_PARAMETERS ffffe000020f6b18    RootHub Endpoint
...
```

在上面的输出中， `ffffe000020f6970 ` 是 **\_ HCD \_ 终结点** 结构的地址。 将此地址传递给 **！ usbkd. usbep**。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

