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
ms.openlocfilehash: e462053b368f6c8de9abd407cd477d22e5ef1643
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372243"
---
# <a name="using-kernel-mode-driver-framework-with-non-pnp-drivers"></a>将内核模式驱动程序框架和非 PnP 驱动程序配合使用





如果你正在编写不支持即插即用 (PnP) 设备的驱动程序，该驱动程序必须：

-   设置[ **WdfDriverInitNonPnpDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags)标记中[ **WDF\_驱动程序\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ns-wdfdriver-_wdf_driver_config)结构的**DriverInitFlags**成员。

-   提供[ *EvtDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)事件回调函数。

-   创建框架设备对象的唯一表示[控制的设备对象](using-control-device-objects.md)。

如果你的设备不支持即插即用，您的驱动程序的作用*不*提供[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。 相反，该驱动程序必须确定是否存在其设备。

 

 





