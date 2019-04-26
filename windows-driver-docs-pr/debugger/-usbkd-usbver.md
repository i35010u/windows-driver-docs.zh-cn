---
title: usbkd.usbver
description: Usbkd.usbver 命令显示 USB 驱动程序堆栈 USBD 接口的版本。
ms.assetid: E3F5A971-64FB-4826-8DC0-59F3615C106A
keywords:
- usbkd.usbver Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a0098679bab02db3486e2dc6f4128231744b3262
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327955"
---
# <a name="usbkdusbver"></a>!usbkd.usbver


**！ Usbkd.usbver**命令显示的 USB 驱动程序堆栈 USBD 接口版本。

```dbgcmd
!usbkd.usbver
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

USBD 接口版本的值存储在变量`usbport!usbd_version`。

<a name="examples"></a>示例
--------

下面是输出的示例 **！ usbkd.usbver**。

```dbgcmd
1: kd> !usbkd.usbver

USBD VER 600 USB stack is VISTA
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

**USBD\_IsInterfaceVersionSupported**
 

 






