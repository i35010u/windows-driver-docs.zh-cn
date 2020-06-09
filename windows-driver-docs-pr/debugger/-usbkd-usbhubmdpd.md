---
title: usbkd.usbhubmdpd
description: 如果在由于 Bug 检查0xFE 生成的故障转储中存在一个 usbkd，则 usbhubmdpd 命令将显示 usbhub _HUB_PORT_DATA 结构。
ms.assetid: 128D45A2-A891-42BC-9E3E-FCDC5B4504A2
keywords:
- usbkd usbhubmdpd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubmdpd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 648d96225bf334b9a709a8e45083c00dd63c539d
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534692"
---
# <a name="usbkdusbhubmdpd"></a>!usbkd.usbhubmdpd


**！ Usbkd. usbhubmdpd**命令显示**usbhub！ \_集线器 \_ 端口 \_ 数据**结构（如果存在于[**Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)中生成的故障转储中）。

```dbgcmd
!usbkd.usbhubmdpd [PortNum]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______PortNum______"></span><span id="_______portnum______"></span><span id="_______PORTNUM______"></span>*PortNum*   
USB 端口号。 如果指定端口号，则此命令将显示表示指定端口的结构（如果存在）。 如果未指定端口号，则此命令将显示在其上启动[**Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)的结构（如果存在）。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd

<a name="remarks"></a>注解
-------

仅当调试因[**Bug 检查0xFE： BUGCODE \_ USB \_ 驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)而生成的故障转储文件时，才使用此命令。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线（USB）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)

 

 






