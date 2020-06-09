---
title: usbkd.usbportmddcontext
description: Usbkd. usbportmddcontext 命令显示 USBPORT 上下文数据，前提是该数据存在于 Bug 检查0xFE 生成的故障转储中。
ms.assetid: 774C7EAE-A33E-49A6-956F-C0791134C221
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
ms.openlocfilehash: 8dc4c5e0a7363598dcee6a9e14f9c45389988330
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534848"
---
# <a name="usbkdusbportmddcontext"></a>!usbkd.usbportmddcontext


如果在由于[**Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)生成的故障转储中存在**usbkd usbportmddcontext**命令，则该命令将显示 USBPORT 上下文数据。

```dbgcmd
!usbkd.usbportmddcontext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd

<a name="remarks"></a>注解
-------

仅当调试因[**Bug 检查0xFE： BUGCODE \_ USB \_ 驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)而生成的故障转储文件时，才使用此命令。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线（USB）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






