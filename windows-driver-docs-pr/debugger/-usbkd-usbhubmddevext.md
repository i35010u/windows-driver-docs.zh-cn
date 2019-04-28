---
title: usbkd.usbhubmddevext
description: Usbkd.usbhubmddevext 命令显示 usbhub _DEVICE_EXTENSION_HUB 结构，如果不存在的 Bug 检查 0xFE 结果作为生成的故障转储中。
ms.assetid: 2A3C1AD4-0537-43B1-BD87-734047D242B9
keywords:
- usbkd.usbhubmddevext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubmddevext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6a7fdfc915c9e7f8040a7c9841897c867ea278b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340621"
---
# <a name="usbkdusbhubmddevext"></a>!usbkd.usbhubmddevext


**！ Usbkd.usbhubmddevext**命令将显示**usbhub ！\_设备\_扩展\_中心**结构，如果已为生成的故障转储中存在[ **Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)。

```dbgcmd
!usbkd.usbhubmddevext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

使用此命令仅在调试时为生成的崩溃转储文件[ **Bug 检查 0xFE:BUGCODE\_USB\_驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






