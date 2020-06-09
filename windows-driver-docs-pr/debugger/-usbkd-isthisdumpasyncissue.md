---
title: usbkd.isthisdumpasyncissue
description: 此命令检查0xFE 崩溃转储文件，以了解故障的可能原因是否是与 USB EHCI 主机控制器关联的 Async 提前问题的中断。
ms.assetid: 1729E52F-F943-4062-94AC-7890C2E25EBF
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
ms.openlocfilehash: a1939efedae2a1a0fbbc3b3d368f3de228b6c2a5
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534050"
---
# <a name="usbkdisthisdumpasyncissue"></a>!usbkd.isthisdumpasyncissue


**！ Usbkd. isthisdumpasyncissue**命令检查由[**Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)生成的故障转储文件，以确定崩溃的可能原因是否是与 USB EHCI 主机控制器关联的 Async 提前问题的中断。

```dbgcmd
!usbkd.isthisdumpasyncissue
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd

<a name="remarks"></a>注解
-------

仅当调试因[**Bug 检查0xFE： BUGCODE \_ USB \_ 驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)而生成的故障转储文件时，才使用此命令。

<a name="examples"></a>示例
--------

下面是 **！ usbkd**的输出示例。

```dbgcmd
1: kd> !analyze -v
*** ...
BUGCODE_USB_DRIVER (fe) 
...
1: kd> !usbkd.isthisdumpasyncissue
This is *NOT* Async on Advance Issue because the EndPointData is NULL
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线（USB）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






