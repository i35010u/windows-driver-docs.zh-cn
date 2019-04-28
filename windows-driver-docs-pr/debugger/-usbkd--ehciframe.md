---
title: usbkd._ehciframe
description: Usbkd._ehciframe 命令显示帧数 FrameListBaseAddress 定期列表条目链索引 EHCI 微型端口。
ms.assetid: 6359FC98-F070-410E-AFE7-C2C67A4F7C98
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
ms.openlocfilehash: 72e79141fb1dd6b34cafe0eb666eea078ac33f35
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335597"
---
# <a name="usbkdehciframe"></a>!usbkd.\_ehciframe


**！ Usbkd。\_ehciframe**的命令显示帧数 EHCI 微型端口 FrameListBaseAddress 定期列表条目链编制索引。

```dbgcmd
!usbkd._ehciframe StructAddr, FrameNumber
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span> *StructAddr*   
地址**usbehci ！\_设备\_数据**结构。

<span id="_______FrameNumber______"></span><span id="_______framenumber______"></span><span id="_______FRAMENUMBER______"></span> *FrameNumber*   
在范围 0 到 1023年的帧数。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






