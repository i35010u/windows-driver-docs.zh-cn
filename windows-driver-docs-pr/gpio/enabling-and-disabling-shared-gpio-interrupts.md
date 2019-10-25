---
title: 启用和禁用共享 GPIO 中断
description: 在某些情况下，来自两个或多个外围设备的中断请求线路可能连接到相同的物理常规用途 i/o （GPIO） pin。 通常为共享中断线路配置用于共享中断线路的 GPIO pin。
ms.assetid: F3C8F2B1-54BC-46A1-8AC2-50006E1156FF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a22c86b1d31edb2cc121941c3024a3278b615df3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825048"
---
# <a name="enabling-and-disabling-shared-gpio-interrupts"></a>启用和禁用共享 GPIO 中断


在某些情况下，来自两个或多个外围设备的中断请求线路可能连接到相同的物理常规用途 i/o （GPIO） pin。 通常为共享中断线路配置用于共享中断线路的 GPIO pin。

如果这些设备的驱动程序注册其中断服务例程（Isr）以在此 GPIO pin 上断言中断时触发，GPIO framework extension （GpioClx）仅在以下情况下调用[*客户端\_EnableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)回调函数第一个驱动程序注册此中断。 当其他驱动程序注册使用已启用的 GPIO 中断时，GpioClx 会内部跟踪这些注册，但不会冗余调用*客户端\_EnableInterrupt*回调函数来启用此中断。 同样，仅当这些注册的最后一个驱动程序释放中断时，GpioClx 才会调用[*客户端\_DisableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)回调函数。

 

 




