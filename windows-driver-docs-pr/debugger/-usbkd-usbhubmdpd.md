---
title: usbkd.usbhubmdpd
description: Usbkd.usbhubmdpd 命令显示 usbhub _HUB_PORT_DATA 结构，如果不存在的 Bug 检查 0xFE 结果作为生成的故障转储中。
ms.assetid: 128D45A2-A891-42BC-9E3E-FCDC5B4504A2
keywords:
- usbkd.usbhubmdpd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd.usbhubmdpd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5a849afa27ddd2e644f3d0fbe62f1ece3594f563
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547986"
---
# <a name="usbkdusbhubmdpd"></a>!usbkd.usbhubmdpd


**！ Usbkd.usbhubmdpd**命令将显示**usbhub ！\_集线器\_端口\_数据**结构，如果已为生成的故障转储中存在[ **Bug 检查 0xFE**](bug-check-0xfe--bugcode-usb-driver.md)。

```dbgcmd
!usbkd.usbhubmdpd [PortNum]
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______PortNum______"></span><span id="_______portnum______"></span><span id="_______PORTNUM______"></span> *PortNum*   
USB 端口号。 如果指定的端口号，此命令显示的结构 （如果存在），表示指定的端口。 如果不指定端口号，此命令将显示在其上 （如果存在） 的结构[ **Bug 检查 0xFE** ](bug-check-0xfe--bugcode-usb-driver.md)已启动。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Usbkd.dll

<a name="remarks"></a>备注
-------

使用此命令仅在调试时为生成的崩溃转储文件[ **Bug 检查 0xFE:BUGCODE\_USB\_驱动程序**](bug-check-0xfe--bugcode-usb-driver.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[通用串行总线 (USB) 驱动程序](https://go.microsoft.com/fwlink/p?LinkID=227351)

 

 






