---
title: usbkd._ehciframe
description: Usbkd._ehciframe 命令显示通过帧号索引的 EHCI 小型端口 FrameListBaseAddress 定期列表条目链。
keywords:
- usbkd._ehciframe Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehciframe
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a7402fb6525d2238bf073250aa1fae7bd36ce16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814657"
---
# <a name="usbkd_ehciframe"></a>！ usbkd。 \_ehciframe


**！ Usbkd。 \_ehciframe** 命令显示以帧号为索引的 EHCI 小型端口 FrameListBaseAddress 定期列表条目链。

```dbgcmd
!usbkd._ehciframe StructAddr, FrameNumber
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbehci 的地址 **！ \_设备 \_ 数据** 结构。

<span id="_______FrameNumber______"></span><span id="_______framenumber______"></span><span id="_______FRAMENUMBER______"></span>*FrameNumber*   
范围0到1023中的帧号。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

