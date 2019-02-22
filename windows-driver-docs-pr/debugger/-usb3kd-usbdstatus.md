---
title: usb3kd.usbdstatus
description: Usb3kd.usbdstatus 扩展显示 USBD 状态代码的名称。
ms.assetid: B79B4E6E-7281-4BB0-9708-23F1462171BB
keywords:
- usb3kd.usbdstatus Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.usbdstatus
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f66742efc8fbb18b9eb51c94d8247354dec7645e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547858"
---
# <a name="usb3kdusbdstatus"></a>!usb3kd.usbdstatus


[ **！ Usb3kd.usbdstatus** ](-usb3kd-device-info.md)扩展显示 USBD 状态代码的名称。

```dbgcmd
!usb3kd.ucx_usbdstatus UrbStatus
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______UsbdStatus______"></span><span id="_______usbdstatus______"></span><span id="_______USBDSTATUS______"></span> *UsbdStatus*   
USBD 状态代码的数值。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

Usb.h 中定义了 USBD 状态代码。

<a name="examples"></a>示例
--------

下面的示例将传递到的数值 0x80000200 **！ usbdstatus**命令。 该命令将返回状态代码，USBD 名称\_状态\_无效\_URB\_函数。

```dbgcmd
3: kd> !usbdstatus 0x80000200
USBD_STATUS_INVALID_URB_FUNCTION (0x80000200)
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






