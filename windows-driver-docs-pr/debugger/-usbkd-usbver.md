---
title: usbkd.usbver
description: Usbkd. usbver 命令显示 USB 驱动程序堆栈的 USBD 接口版本。
keywords:
- usbkd usbver Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d70d0451fb88a25db54328813fd8f17f07185b11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833861"
---
# <a name="usbkdusbver"></a>!usbkd.usbver


**！ Usbkd. usbver** 命令显示 USB 驱动程序堆栈的 USBD 接口版本。

```dbgcmd
!usbkd.usbver
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

USBD 接口版本的值存储在变量中 `usbport!usbd_version` 。

<a name="examples"></a>示例
--------

下面是 **！ usbkd** 的输出示例。

```dbgcmd
1: kd> !usbkd.usbver

USBD VER 600 USB stack is VISTA
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

**USBD \_ IsInterfaceVersionSupported**
 

