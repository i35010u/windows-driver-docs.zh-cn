---
title: usbkd _ehciframe
description: _Ehciframe usbkd 命令显示一个 EHCI 小型端口 FrameListBaseAddress 定期列表条目链，并按帧号进行索引。
ms.assetid: 6359FC98-F070-410E-AFE7-C2C67A4F7C98
keywords:
- usbkd _ehciframe Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehciframe
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7052fd160a57c80e347eadc4931b2736f81a20a3
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534882"
---
# <a name="usbkd_ehciframe"></a>！ usbkd。 \_ehciframe


**！ Usbkd。 \_ehciframe**命令显示以帧号为索引的 EHCI 小型端口 FrameListBaseAddress 定期列表条目链。

```dbgcmd
!usbkd._ehciframe StructAddr, FrameNumber
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbehci 的地址 **！ \_设备 \_ 数据**结构。

<span id="_______FrameNumber______"></span><span id="_______framenumber______"></span><span id="_______FRAMENUMBER______"></span>*FrameNumber*   
范围0到1023中的帧号。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线（USB）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






