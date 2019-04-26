---
title: 将内核模式驱动程序框架和非 PnP 驱动程序配合使用
description: 将内核模式驱动程序框架和非 PnP 驱动程序配合使用
ms.assetid: b4b6add2-0e27-4af7-b6bf-5e47db7db560
keywords:
- 非 PnP 驱动程序 WDK KMDF
- 内核模式驱动程序 WDK KMDF，即插即用
- KMDF WDK，即插即用
- 内核模式驱动程序框架 WDK，即插即用
- 插 WDK KMDF，非 PnP 驱动程序
- 即插即用 WDK KMDF，非 PnP 驱动程序
- 基于框架的驱动程序 WDK KMDF，即插即用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7e7efa27b548eb26917092f6463d1f63470fb2e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327321"
---
# <a name="using-kernel-mode-driver-framework-with-non-pnp-drivers"></a>将内核模式驱动程序框架和非 PnP 驱动程序配合使用





如果你正在编写不支持即插即用 (PnP) 设备的驱动程序，该驱动程序必须：

-   设置[ **WdfDriverInitNonPnpDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff551303)标记中[ **WDF\_驱动程序\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551300)结构的**DriverInitFlags**成员。

-   提供[ *EvtDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff541694)事件回调函数。

-   创建框架设备对象的唯一表示[控制的设备对象](using-control-device-objects.md)。

如果你的设备不支持即插即用，您的驱动程序的作用*不*提供[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数。 相反，该驱动程序必须确定是否存在其设备。

 

 





