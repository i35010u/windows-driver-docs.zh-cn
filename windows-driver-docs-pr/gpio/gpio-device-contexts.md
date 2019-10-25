---
title: GPIO 设备上下文
description: 常规用途 i/o （GPIO）控制器设备由框架设备对象表示。
ms.assetid: 4BE99C71-9BA6-44E3-A54F-DE8C3440A474
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16cab2778277b72eebc1ecde941a47baa17dba0f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824995"
---
# <a name="gpio-device-contexts"></a>GPIO 设备上下文


常规用途 i/o （GPIO）控制器设备由框架设备对象表示。 GPIO 控制器驱动程序可以将设备上下文与此设备对象相关联。 驱动程序使用此设备上下文来持久存储有关 GPIO 控制器设备状态的信息。

当 GPIO framework 扩展（GpioClx）调用由驱动程序实现的事件回调函数时，GpioClx 会将设备上下文作为参数传递给此函数。 回调函数检查设备上下文以确定设备的当前状态。 如果该函数更改了此状态，则会相应地更新设备上下文。

GpioClx 为设备对象分配存储。 如果 GPIO 控制器驱动程序具有多个设备对象，则每个对象的设备上下文都是相同的大小。 在[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程期间，驱动程序将调用[**GPIO\_CLX\_RegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_registerclient)方法来注册其回调函数并指定其所需的设备上下文大小。 稍后，在[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调例程期间，驱动程序将调用[**GPIO\_CLX\_ProcessAddDevicePostDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_processadddevicepostdevicecreate)方法，将新设备对象传递给 GpioClx，GpioClx 为此对象. 此后，当 GpioClx 调用驱动程序实现的回调函数时，此设备上下文将作为参数传递给函数。

 

 




