---
title: usbkd.usbver
description: Usbkd. usbver 命令显示 USB 驱动程序堆栈的 USBD 接口版本。
ms.assetid: E3F5A971-64FB-4826-8DC0-59F3615C106A
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
ms.openlocfilehash: 6c1fe4efe0c3c24c623e6e34819e5210a5a2ffb4
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533974"
---
# <a name="usbkdusbver"></a>!usbkd.usbver


**！ Usbkd. usbver**命令显示 USB 驱动程序堆栈的 USBD 接口版本。

```dbgcmd
!usbkd.usbver
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd

<a name="remarks"></a>注解
-------

USBD 接口版本的值存储在变量中 `usbport!usbd_version` 。

<a name="examples"></a>示例
--------

下面是 **！ usbkd**的输出示例。

```dbgcmd
1: kd> !usbkd.usbver

USBD VER 600 USB stack is VISTA
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线（USB）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

**USBD \_ IsInterfaceVersionSupported**
 

 






