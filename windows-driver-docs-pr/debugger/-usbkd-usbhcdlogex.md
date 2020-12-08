---
title: usbkd.usbhcdlogex
description: Usbkd. usbhcdlogex 命令显示 USB 主机控制器的带批注调试日志。
keywords:
- usbkd usbhcdlogex Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhcdlogex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8946ccd16976f1d8ea5c5d3c474a5d46755082d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818681"
---
# <a name="usbkdusbhcdlogex"></a>!usbkd.usbhcdlogex


**！ Usbkd. usbhcdlogex** 命令显示 USB 主机控制器的带批注调试日志。

```dbgcmd
!usbkd.usbhcdlogex DeviceExtension[, NumberOfEntries]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span>*DeviceExtension*   
功能设备对象的设备扩展地址 (UHCI 或 EHCI USB 主机控制器的 FDO) 。

<span id="_______NumberOfEntries______"></span><span id="_______numberofentries______"></span><span id="_______NUMBEROFENTRIES______"></span>*NumberOfEntries*   
要显示的日志条目数。 若要显示整个日志，请将此参数设置为-1。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种查找 USB 主机控制器的 FDO 的设备扩展地址的方法。 首先输入 [**！ usbkd. usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0 kd> !usbkd.usb2tree

EHCI MINIPORT(s) dt usbport!_USBPORT_MINIPORT_DRIVER ffffe00001f48bd0
...

2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
...
```

在上面的输出中，FDO 的设备扩展的地址显示为 [DML](debugger-markup-language-commands.md) 命令 **！ ehci \_ info ffffe00001ca11a0** 的参数。

现在，将设备扩展的地址传递给 **！ usbhcdlogex** 命令。 在此示例中，第二个参数将显示范围限制为20个日志条目。

```dbgcmd
0: kd> !usbkd.usbhcdlogex ffffe00001ca11a0, 20
LOG@: ffffe00001ca11b8 
>LOG mask = 3ff idx = fff68e95 (295)
*LOG: ffffe000020192a0  LOGSTART: ffffe00002014000 *LOGEND: ffffe0000201bfe0 # 20 
[ 000] ffffe000020192a0 xSt0 ffffe00001ca1b88 0000000000000006 0000000000000001 
[ 001] ffffe000020192c0 xnd8 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
[ 002] ffffe000020192e0 xnd0 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
//
// USBPORT_Xdpc_End()    - USBPORT_Core_UsbHcIntDpc_Worker() DPC/XDPC: 2 of 4

[ 003] ffffe00002019300 gNX0 0000000000000000 0000000000000000 ffffe00001ca1b88 
[ 004] ffffe00002019320 xbg1 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
[ 005] ffffe00002019340 xbg0 ffffe00001ca1b88 ffffe00001ca1050 ffffe00001ca22e8 
//
// USBPORT_Xdpc_iBegin() - USBPORT_Core_UsbHcIntDpc_Worker() DPC/XDPC: 2 of 4

[ 006] ffffe00002019360 tmo4 0000000000000000 0000000000000040 ffffe00001ca1c20 
[ 007] ffffe00002019380 tmo3 0000000000000000 0000000000989680 ffffe00001ca1c20 
[ 008] ffffe000020193a0 tmo2 0000000000000000 00000000000003e8 ffffe00001ca1c20 
[ 009] ffffe000020193c0 tmo1 0000000000000000 000000000002625a ffffe00001ca1c20 
[ 010] ffffe000020193e0 tmo0 00000000000003e8 ffffe00001ca1b88 ffffe00001ca1c20 
[ 011] ffffe00002019400 hci0 0000000000000000 0000000000000000 0000000000000000 
[ 012] ffffe00002019420 xSt0 ffffe00001ca1b88 0000000000000008 0000000000000003 
[ 013] ffffe00002019440 xdw4 ffffe00001ca1b88 0000000000000000 0000000000000000 
[ 014] ffffe00002019460 xdw2 ffffe00001ca1b88 ffffe00001ca1050 0000000000000002 
[ 015] ffffe00002019480 xdB0 ffffe00001ca1b88 ffffe00001ca1050 0000000000000000 
//
// USBPORT_Xdpc_Worker_HcIntDpc()  DPC/XDPC: 2 of 4

[ 016] ffffe000020194a0 iDP- 0000000000000000 0000000000b73e26 0000000000000000 
//
// USBPORT_IsrDpc() - Exit()

[ 017] ffffe000020194c0 xSt0 ffffe00001ca1b88 0000000000000007 0000000000000002 
[ 018] ffffe000020194e0 Xsi1 ffffe00001ca1b88 0000000000000000 0000000000000000 
//
// USBPORT_Xdpc_iSignal()- USBPORT_Core_UsbHcIntDpc_Worker() DPC/XDPC: 2 of 4

[ 019] ffffe00002019500 chgZ 0000000000000000 0000000000b73e26 0000000000000000 
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

