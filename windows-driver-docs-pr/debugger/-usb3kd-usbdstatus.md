---
title: usb3kd.usbdstatus
description: Usb3kd. usbdstatus 扩展显示 USBD 状态代码的名称。
ms.assetid: B79B4E6E-7281-4BB0-9708-23F1462171BB
keywords:
- usb3kd usbdstatus Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usb3kd.usbdstatus
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aa6ddf453d1f363bad6f877ac8289f91af719d5c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212263"
---
# <a name="usb3kdusbdstatus"></a>!usb3kd.usbdstatus


[**！ Usb3kd usbdstatus**](-usb3kd-device-info.md)扩展显示 USBD 状态代码的名称。

```dbgcmd
!usb3kd.ucx_usbdstatus UrbStatus
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______UsbdStatus______"></span><span id="_______usbdstatus______"></span><span id="_______USBDSTATUS______"></span>*UsbdStatus*   
USBD 状态代码的数值。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usb3kd.dll

<a name="remarks"></a>备注
-------

USBD 状态代码在中定义。

<a name="examples"></a>示例
--------

下面的示例将数值0x80000200 传递给 **！ usbdstatus** 命令。 该命令返回状态代码的名称，USBD \_ status \_ \_ URB \_ 函数无效。

```dbgcmd
3: kd> !usbdstatus 0x80000200
USBD_STATUS_INVALID_URB_FUNCTION (0x80000200)
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 3.0 扩展](usb-3-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

