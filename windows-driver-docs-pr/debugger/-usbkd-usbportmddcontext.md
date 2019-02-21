---
title: usbkd.usbportmddcontext
description: 如果处在 Bug 后生成的故障转储，检查 0xFE usbkd.usbportmddcontext 命令显示 USBPORT 上下文数据。
ms.assetid: 774C7EAE-A33E-49A6-956F-C0791134C221
keywords:
- usbkd.usbportmddcontext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbportmddcontext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b50928970c5041158147bed443dedd2fc8a850d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519853"
---
# <a name="usbkdusbportmddcontext"></a>!usbkd.usbportmddcontext


**！ Usbkd.usbportmddcontext**命令显示 USBPORT 上下文数据，如果它为生成的故障转储中存在[ **Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)。

```dbgcmd
!usbkd.usbportmddcontext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

使用此命令仅在调试时为生成的崩溃转储文件[ **Bug 检查 0xFE:BUGCODE\_USB\_驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






