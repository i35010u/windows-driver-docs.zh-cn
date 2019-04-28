---
title: usbkd._ehciqh
description: Usbkd._ehciqh 命令显示 usbehci _HCD_QUEUEHEAD_DESCRIPTOR 结构中的信息。
ms.assetid: 52A1CF03-3B1D-4CC6-A4DD-3E73A7AB2F00
keywords:
- usbkd._ehciqh Windows Debugging
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehciqh
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d43bef72e1d3aaa8b1e71d2ac77e6851a1bab6fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335590"
---
# <a name="usbkdehciqh"></a>!usbkd.\_ehciqh


**！ Usbkd。\_ehciqh**命令将显示从信息**usbehci ！\_HCD\_QUEUEHEAD\_描述符**结构。 使用此命令显示有关异步终结点 （即，控制和大容量的终结点） 的信息。

```dbgcmd
!usbkd._ehciqh StructAddr
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
地址**usbehci ！\_HCD\_QUEUEHEAD\_描述符**结构。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






