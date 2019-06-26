---
title: GPIO 设备上下文
description: 常规用途的 I/O (GPIO) 控制器设备由 framework 设备对象表示。
ms.assetid: 4BE99C71-9BA6-44E3-A54F-DE8C3440A474
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d44735cdb30c336c2f57b585b77488494c6865a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363601"
---
# <a name="gpio-device-contexts"></a>GPIO 设备上下文


常规用途的 I/O (GPIO) 控制器设备由 framework 设备对象表示。 GPIO 控制器驱动程序可以将此设备对象与关联的设备上下文。 驱动程序使用此设备上下文以永久存储 GPIO 控制器设备的状态信息。

当 GPIO 框架扩展 (GpioClx) 调用时由驱动程序实现一个事件回调函数时，GpioClx 设备上下文给此函数将作为参数传递。 该回调函数将检查设备上下文以确定设备的当前状态。 如果该函数将更改此状态，它将相应地更新设备上下文。

GpioClx 设备对象分配存储。 如果 GPIO 控制器驱动程序具有多个设备对象，每个对象的设备上下文是相同的大小。 期间[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程，驱动程序将调用[ **GPIO\_CLX\_RegisterClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_registerclient)若要注册其回调函数，并指定它需要的设备上下文大小的方法。 更高版本，期间[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调例程，驱动程序将调用[ **GPIO\_CLX\_ProcessAddDevicePostDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_processadddevicepostdevicecreate)方法将新的设备对象传递到 GpioClx 和 GpioClx 此对象分配的设备上下文。 此后，当 GpioClx 调用驱动程序实现回调函数时，此设备上下文被传递到该函数作为参数。

 

 




