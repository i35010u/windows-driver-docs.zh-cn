---
title: usbkd.usbportmddcontext
description: Usbkd. usbportmddcontext 命令显示 USBPORT 上下文数据，前提是该数据存在于 Bug 检查0xFE 生成的故障转储中。
keywords:
- usbkd usbportmddcontext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbportmddcontext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 57a8691048b4cc98f6c880f03d89acdde79ff97f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833891"
---
# <a name="usbkdusbportmddcontext"></a>!usbkd.usbportmddcontext


如果在由于 [**Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)生成的故障转储中存在 **usbkd usbportmddcontext** 命令，则该命令将显示 USBPORT 上下文数据。

```dbgcmd
!usbkd.usbportmddcontext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

仅当调试因 [**Bug 检查0xFE： BUGCODE \_ USB \_ 驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)而生成的故障转储文件时，才使用此命令。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

