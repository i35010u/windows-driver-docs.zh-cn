---
title: usbkd.isthisdumpasyncissue
description: 此命令检查0xFE 崩溃转储文件，以了解故障的可能原因是否是与 USB EHCI 主机控制器关联的 Async 提前问题的中断。
keywords:
- usbkd isthisdumpasyncissue Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.isthisdumpasyncissue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eac7bce3102cc565ea2281abbfc8423ed72a6148
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836902"
---
# <a name="usbkdisthisdumpasyncissue"></a>!usbkd.isthisdumpasyncissue


**！ Usbkd. isthisdumpasyncissue** 命令检查由 [**Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)生成的故障转储文件，以确定崩溃的可能原因是否是与 USB EHCI 主机控制器关联的 Async 提前问题的中断。

```dbgcmd
!usbkd.isthisdumpasyncissue
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

仅当调试因 [**Bug 检查0xFE： BUGCODE \_ USB \_ 驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)而生成的故障转储文件时，才使用此命令。

<a name="examples"></a>示例
--------

下面是 **！ usbkd** 的输出示例。

```dbgcmd
1: kd> !analyze -v
**_ ...
BUGCODE_USB_DRIVER (fe) 
...
1: kd> !usbkd.isthisdumpasyncissue
This is _NOT* Async on Advance Issue because the EndPointData is NULL
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

