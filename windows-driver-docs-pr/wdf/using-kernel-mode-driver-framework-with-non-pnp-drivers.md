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
ms.openlocfilehash: 7afb5e0cfb200905de55cdd41271e61e9ec1298b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845436"
---
# <a name="using-kernel-mode-driver-framework-with-non-pnp-drivers"></a>将内核模式驱动程序框架和非 PnP 驱动程序配合使用





如果为不支持即插即用（PnP）的设备编写驱动程序，则驱动程序必须：

-   在[**WDF\_驱动程序\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)结构的**DriverInitFlags**成员中设置[**WdfDriverInitNonPnpDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags)标志。

-   提供[*EvtDriverUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)事件回调函数。

-   创建仅代表[控制设备对象](using-control-device-objects.md)的框架设备对象。

如果你的设备不支持 PnP，你的驱动程序将*不*提供[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数。 相反，驱动程序必须确定其设备是否存在。

 

 





