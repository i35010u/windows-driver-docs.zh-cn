---
title: usbkd.usbdstatus
description: Usbkd.usbdstatus 命令显示 USBD 状态代码的名称。
ms.assetid: 9983433E-1D17-47C6-972B-0A02B228A6AE
keywords:
- usbkd.usbdstatus Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbdstatus
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed253e89d357651d2eb5dc6106ebb3adb2ab1c1d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562688"
---
# <a name="usbkdusbdstatus"></a>!usbkd.usbdstatus


**！ Usbkd.usbdstatus**命令显示 USBD 状态代码的名称。

```dbgcmd
!usbkd.usbdstatus StatusCode
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StatusCode______"></span><span id="_______statuscode______"></span><span id="_______STATUSCODE______"></span> *StatusCode*   
USBD 状态代码的十六进制值。 Usb.h 中定义了这些代码。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是输出的示例 **！ usbdstatus**。

```dbgcmd
1: kd> !usbkd.usbdstatus 0xC0000008

USBD_STATUS_DATA_OVERRUN (0xC0000008)
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






