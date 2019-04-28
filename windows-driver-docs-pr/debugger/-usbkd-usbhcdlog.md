---
title: usbkd.usbhcdlog
description: Usbkd.usbhcdlog 命令显示有关 USB 主控制器的调试日志的一部分。
ms.assetid: 78FDC557-7791-422A-AB7B-5C9B6A1DF481
keywords:
- usbkd.usbhcdlog Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdlog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 508a0b6f751c70bcacecdc1607d8c6e5e687eac8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330844"
---
# <a name="usbkdusbhcdlog"></a>!usbkd.usbhcdlog


[ **！ Usbkd.usbhcdlog** ](https://msdn.microsoft.com/library/windows/hardware/dn367076)命令显示有关 USB 主控制器的调试日志的一部分。

```dbgcmd
!usbkd.usbhcdlog DeviceExtension[, NumberOfEntries]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
适用于 UHCI 或 EHCI USB 主控制器的功能的设备对象 (FDO) 的设备扩展的地址。

<span id="_______NumberOfEntries______"></span><span id="_______numberofentries______"></span><span id="_______NUMBEROFENTRIES______"></span> *NumberOfEntries*   
若要显示的日志条目数。 若要显示整个日志，请将此参数设置为-1。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种方法找到的 USB 主控制器 FDO 设备扩展的地址。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0 kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0
...

2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

在上面的输出，FDO 设备扩展的地址显示为的参数[DML](debugger-markup-language-commands.md)命令 **！ ehci\_信息 ffffe00001ca11a0**。

现在将传递到设备扩展的地址 **！ usbhcdlog**命令。 在此示例中，第二个参数将显示限制为四个日志条目。

```dbgcmd
0: kd> !usbkd.usbhcdlog ffffe00001ca11a0, 4

LOG@: ffffe00001ca11b8 
>LOG mask = 3ff idx = fff68e95 (295)
*LOG: ffffe000020192a0  LOGSTART: ffffe00002014000 *LOGEND: ffffe0000201bfe0 # 4 
[ 000] ffffe000020192a0 xSt0 ffffe00001ca1b88 0000000000000006 0000000000000001 
[ 001] ffffe000020192c0 xnd8 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
[ 002] ffffe000020192e0 xnd0 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
[ 003] ffffe00002019300 gNX0 0000000000000000 0000000000000000 ffffe00001ca1b88 
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






