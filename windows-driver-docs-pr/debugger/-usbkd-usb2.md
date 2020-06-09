---
title: usbkd
description: Usbkd 命令显示了包含 USB 2.0 计划信息的 USB 终结点的列表。
ms.assetid: 48DC685A-3624-4DAD-8077-FB7C4BE4BE93
keywords:
- usbkd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usb2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7e00df26d319510bcfd7c5e729a60d75a7411d3e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534038"
---
# <a name="usbkdusb2"></a>!usbkd.usb2


**！ Usbkd**命令显示了包含 usb 2.0 计划信息的 usb 终结点的列表。

```dbgcmd
!usbkd.usb2 DeviceExtension
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*DeviceExtension*   
USB 主机控制器的功能设备对象（FDO）的设备扩展的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd

<a name="examples"></a>示例
--------

下面是一种查找 USB 主机控制器的 FDO 的设备扩展地址的方法。 首先输入[**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

在上面的输出中，FDO 的设备扩展的地址显示为[DML](debugger-markup-language-commands.md)命令 **！ ehci \_ info ffffe00001ca11a0**的参数。 将设备扩展的地址传递给 **！ usb2**命令。

```dbgcmd
0: kd> !usbkd.usb2 ffffe00001ca11a0

Sig: HFDO
Hcd FDO Extension:
----------
----------
dt usbport!_HCD_ENDPOINT ffffe0000212d970  !usbep ffffe0000212d970
    Tt 0000000000000000 Device Address: 0x00, ep 0x81 Interrupt In
    dt _USB2LIB_ENDPOINT_CONTEXT ffffe000023b60f0    dt _USB2_EP ffffe000023b6100
    Period,offset,Ordinal(32,0,0)   smask,cmask(00,00  ........ , ........) maxpkt 1
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线（USB）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






