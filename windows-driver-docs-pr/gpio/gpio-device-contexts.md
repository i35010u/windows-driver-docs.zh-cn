---
title: GPIO 设备上下文
description: 常规用途 i/o (GPIO) 控制器设备由框架设备对象表示。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf948359289fe7a0281addd167654358f329ef3e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830609"
---
# <a name="gpio-device-contexts"></a>GPIO 设备上下文


常规用途 i/o (GPIO) 控制器设备由框架设备对象表示。 GPIO 控制器驱动程序可以将设备上下文与此设备对象相关联。 驱动程序使用此设备上下文来持久存储有关 GPIO 控制器设备状态的信息。

当 GPIO framework 扩展 (GpioClx) 调用由驱动程序实现的事件回调函数时，GpioClx 会将设备上下文作为参数传递给此函数。 回调函数检查设备上下文以确定设备的当前状态。 如果该函数更改了此状态，则会相应地更新设备上下文。

GpioClx 为设备对象分配存储。 如果 GPIO 控制器驱动程序具有多个设备对象，则每个对象的设备上下文都是相同的大小。 在 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程期间，驱动程序将调用 [**GPIO \_ CLX \_ RegisterClient**](/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_registerclient) 方法来注册其回调函数并指定其所需的设备上下文大小。 稍后，在 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调例程期间，驱动程序将调用 [**GPIO \_ CLX \_ ProcessAddDevicePostDeviceCreate**](/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_processadddevicepostdevicecreate) 方法，以将新设备对象传递给 GpioClx，GpioClx 为此对象分配设备上下文。 此后，当 GpioClx 调用驱动程序实现的回调函数时，此设备上下文将作为参数传递给函数。

 

