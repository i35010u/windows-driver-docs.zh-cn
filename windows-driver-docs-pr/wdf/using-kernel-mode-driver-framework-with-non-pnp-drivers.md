---
title: 将内核模式驱动程序框架和非 PnP 驱动程序配合使用
description: 将内核模式驱动程序框架和非 PnP 驱动程序配合使用
ms.assetid: b4b6add2-0e27-4af7-b6bf-5e47db7db560
keywords:
- 非 PnP 驱动程序 WDK KMDF
- 内核模式驱动程序 WDK KMDF、PnP
- KMDF WDK、PnP
- 内核模式驱动程序框架 WDK、PnP
- 即插即用 WDK KMDF，非 PnP 驱动程序
- PnP WDK KMDF，非 PnP 驱动程序
- 基于框架的驱动程序 WDK KMDF，PnP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dd268014fc2195cc7e1eea8a21a46150b47a608
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185705"
---
# <a name="using-kernel-mode-driver-framework-with-non-pnp-drivers"></a>将内核模式驱动程序框架和非 PnP 驱动程序配合使用





如果为不支持 (PnP) 即插即用的设备编写驱动程序，则驱动程序必须：

-   在[**WDF \_ 驱动程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)结构的**DriverInitFlags**成员中设置[**WdfDriverInitNonPnpDriver**](/windows-hardware/drivers/ddi/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags)标志。

-   提供 [*EvtDriverUnload*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload) 事件回调函数。

-   创建仅代表 [控制设备对象](using-control-device-objects.md)的框架设备对象。

如果你的设备不支持 PnP，你的驱动程序将 *不* 提供 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数。 相反，驱动程序必须确定其设备是否存在。

 

