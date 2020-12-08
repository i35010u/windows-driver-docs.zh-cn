---
title: usbkd.usbdstatus
description: Usbkd. usbdstatus 命令显示 USBD 状态代码的名称。
keywords:
- usbkd usbdstatus Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbdstatus
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5a6123a976b52cf39e052ed1417bad40c93203b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820383"
---
# <a name="usbkdusbdstatus"></a>!usbkd.usbdstatus


**！ Usbkd. usbdstatus** 命令显示 USBD 状态代码的名称。

```dbgcmd
!usbkd.usbdstatus StatusCode
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StatusCode______"></span><span id="_______statuscode______"></span><span id="_______STATUSCODE______"></span>*StatusCode*   
USBD 状态代码的十六进制值。 这些代码是在 usb 中定义的。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是 **！ usbdstatus** 的输出示例。

```dbgcmd
1: kd> !usbkd.usbdstatus 0xC0000008

USBD_STATUS_DATA_OVERRUN (0xC0000008)
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

