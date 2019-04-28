---
title: usbkd.usbhublog
description: Usbkd.usbhublog 命令显示的 USB 集线器的调试日志。
ms.assetid: DFDF595E-3452-40C2-A6C7-94FB8954002C
keywords:
- usbkd.usbhublog Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhublog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 75a1c337e4e50da85b10860b05d113f122845497
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340617"
---
# <a name="usbkdusbhublog"></a>!usbkd.usbhublog


**！ Usbkd.usbhublog**命令显示的 USB 集线器的调试日志。

```dbgcmd
!usbkd.usbhublog DeviceExtension[, NumberOfEntries]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______DeviceExtension______"></span><span id="_______deviceextension______"></span><span id="_______DEVICEEXTENSION______"></span> *DeviceExtension*   
适用于 USB 集线器的功能的设备对象 (FDO) 的设备扩展的地址。

<span id="_______NumberOfEntries______"></span><span id="_______numberofentries______"></span><span id="_______NUMBEROFENTRIES______"></span> *NumberOfEntries*   
若要显示的日志条目数。 若要显示整个日志，请将此参数设置为-1。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是一种方法找到的 USB 集线器 FDO 设备扩展的地址。 首次进入[ **！ usbkd.usb2tree**](-usbkd-usb2tree.md)。

```dbgcmd
0: kd> !usbkd.usb2tree
...
2)!ehci_info ffffe00001ca11a0 !devobj ffffe00001ca1050 PCI: VendorId 8086 DeviceId 293c RevisionId 0002 
    RootHub !hub2_info ffffe000023201a0 !devstack ffffe00002320050
      ...
```

在上面的输出中可以看到建议的命令 **！ devstack ffffe00002320050**。 输入此命令。

```dbgcmd
0: kd> !kdexts.devstack ffffe00002320050

  !DevObj           !DrvObj            !DevExt           ObjectName
> ffffe00002320050  \Driver\usbhub     ffffe000023201a0  0000002d
  ffffe0000213c050  \Driver\usbehci    ffffe0000213c1a0  USBPDO-3
...
```

在上面的输出，`ffffe000023201a0`为中心的 FDO 是设备扩展的地址。

现在将传递到设备扩展的地址 **！ usbhublog**。 在此示例中，第二个参数将显示限制为 10 个日志条目。

```dbgcmd
0: kd> !usbkd.usbhublog ffffe000023201a0, 10

LOG@: ffffe000023201a0 (usbhub!_DEVICE_EXTENSION_HUB)
>LOG mask = ff idx = ffffa333 (33)
*LOG: ffffe00002321ca0  LOGSTART: ffffe00002321640 *LOGEND: ffffe00002323620 # 20 
[ 000] ffffe00002321ca0 HDec 0000000000000000 ffffe000002904d0 0000000000000001 
[ 001] ffffe00002321cc0 HPCd 0000000000000000 0000000000000002 0000000000000004 
[ 002] ffffe00002321ce0 qwk- 0000000000000000 ffffe000021c11c0 0000000000000000 
[ 003] ffffe00002321d00 pq-- 0000000000000000 0000000000000002 0000000000000004 
[ 004] ffffe00002321d20 _6p4 0000000000000000 0000000000000000 0000000000000004 
[ 005] ffffe00002321d40 _6p1 0000000000000000 0000000000000003 0000000000000004 
[ 006] ffffe00002321d60 pq++ 0000000000000000 0000000000000003 0000000000000004 
[ 007] ffffe00002321d80 pq++ 0000000000000000 0000000000000006 0000000000000004 
[ 008] ffffe00002321da0 _6p0 0000000000000000 ffffe000021c11c0 0000000000000004 
[ 009] ffffe00002321dc0 pqDP 0000000000000000 ffffe000021c11d8 0000000000000006
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






