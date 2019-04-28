---
title: usbkd.isthisdumpasyncissue
description: 此命令将检查 0xFE 崩溃转储文件，来查看故障的可能原因是否与 USB EHCI 主机控制器相关联的异步提前问题上中断。
ms.assetid: 1729E52F-F943-4062-94AC-7890C2E25EBF
keywords:
- usbkd.isthisdumpasyncissue Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.isthisdumpasyncissue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b7799b3ecc66f8b22deab723b144a3a46293efc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334098"
---
# <a name="usbkdisthisdumpasyncissue"></a>!usbkd.isthisdumpasyncissue


**！ Usbkd.isthisdumpasyncissue**命令将检查生成的崩溃转储文件[ **Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)，以查看是否在发生崩溃的可能原因上已中断异步提前与 USB EHCI 主机控制器相关联的问题。

```dbgcmd
!usbkd.isthisdumpasyncissue
```

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

使用此命令仅在调试时为生成的崩溃转储文件[ **Bug 检查 0xFE:BUGCODE\_USB\_驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)。

<a name="examples"></a>示例
--------

下面是输出的示例 **！ usbkd.isthisdumpasyncissue**。

```dbgcmd
1: kd> !analyze -v
*** ...
BUGCODE_USB_DRIVER (fe) 
...
1: kd> !usbkd.isthisdumpasyncissue
This is *NOT* Async on Advance Issue because the EndPointData is NULL
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






