---
title: usbkd.usbhubmddevext
description: 如果在由于 Bug 检查0xFE 生成的故障转储中存在一个 usbkd，则 usbhubmddevext 命令将显示 usbhub _DEVICE_EXTENSION_HUB 结构。
keywords:
- usbkd usbhubmddevext Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubmddevext
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c88ad6f5dc147fd24d46c258544398b016d9e9ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829761"
---
# <a name="usbkdusbhubmddevext"></a>!usbkd.usbhubmddevext


**！ Usbkd. usbhubmddevext** 命令显示 **usbhub！ \_如果 \_ \_** 在由于 [**Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)而生成的故障转储中存在一个，则为设备扩展中心结构。

```dbgcmd
!usbkd.usbhubmddevext
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

仅当调试因 [**Bug 检查0xFE： BUGCODE \_ USB \_ 驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)而生成的故障转储文件时，才使用此命令。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

