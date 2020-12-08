---
title: 启用和禁用共享 GPIO 中断
description: 在某些情况下，两个或多个外围设备的中断请求线路可能会连接到相同的物理常规用途 i/o (GPIO) pin。 通常为共享中断线路配置用于共享中断线路的 GPIO pin。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 409b24c7503a0edbcaeb42c8f496121516e0abda
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830621"
---
# <a name="enabling-and-disabling-shared-gpio-interrupts"></a>启用和禁用共享 GPIO 中断


在某些情况下，两个或多个外围设备的中断请求线路可能会连接到相同的物理常规用途 i/o (GPIO) pin。 通常为共享中断线路配置用于共享中断线路的 GPIO pin。

如果这些设备的驱动程序将 (Isr) 的中断服务例程注册为在此 GPIO pin 上断言中断时触发，则 GPIO framework extension (GpioClx) 仅在第一个驱动程序注册此中断时才会调用 [*客户端 \_ EnableInterrupt*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt) 回调函数。 当其他驱动程序注册使用已启用的 GPIO 中断时，GpioClx 将在内部跟踪这些注册，但不会冗余地调用 *客户端 \_ EnableInterrupt* 回调函数来启用此中断。 同样，仅当这些已注册的最后一个驱动程序释放中断时，GpioClx 才会调用 [*客户端 \_ DisableInterrupt*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt) 回调函数。

 

