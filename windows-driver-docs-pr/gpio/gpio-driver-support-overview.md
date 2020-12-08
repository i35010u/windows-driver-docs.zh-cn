---
title: GPIO 驱动程序支持概述
description: 从 Windows 8 开始，GPIO 框架扩展 (GpioClx) 简化了为 GPIO 控制器设备编写驱动程序的任务。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2dbacbe4dd2e4eb3e543751ce7016ae6d299b94
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801795"
---
# <a name="gpio-driver-support-overview"></a>GPIO 驱动程序支持概述


从 Windows 8 开始，GPIO 框架扩展 (GpioClx) 简化了为 GPIO 控制器设备编写驱动程序的任务。 另外，GpioClx 还为连接到 GPIO 引脚的外围设备提供驱动程序支持。 GpioClx 是系统提供的针对内核模式驱动程序框架 (KMDF) 的扩展，其执行的处理任务对于 GPIO 设备类的成员来说很常见。

本概述讨论了下列主题：

- [GPIO 驱动程序支持概述](#gpio-driver-support-overview)
    - [GPIO 控制器驱动程序](#gpio-controller-drivers)
    - [使用 GPIO Pin 的外围设备的驱动程序](#drivers-for-peripheral-devices-that-use-gpio-pins)

## <a name="gpio-controller-drivers"></a>GPIO 控制器驱动程序


硬件供应商提供驱动程序来控制其 GPIO 控制器。 GPIO 控制器驱动程序是 KMDF 驱动程序，用于管理 GPIO 控制器的所有特定于硬件的操作。 GPIO 控制器驱动程序与 GpioClx 会，用于处理配置为数据输入和数据输出的 GPIO 引脚组的 i/o 请求。 此外，此驱动程序与 GpioClx 会，以处理配置为中断输入的 GPIO pin 发出的中断请求。

GPIO 控制器设备具有一定数量的 GPIO pin。 这些针脚可以物理连接到外围设备。 GPIO pin 可以配置为数据输入、数据输出或中断请求输入。 通常，GPIO pin 专用于外围设备，而不是由两个或多个设备共享。 GPIO pin 和外围设备之间的连接是固定的，用户不能对其进行更改 (例如，通过删除外围设备并将其替换为另一个设备) 。 因此，可以在平台固件中介绍如何将 GPIO pin 分配给外围设备。




下图显示了 GPIO 控制器驱动程序和 GpioClx。

![gpio 组件框图](images/gpiomodules.png)

GPIO 控制器驱动程序和 GpioClx 通过 GpioClx 设备驱动程序接口 (DDI) 彼此进行通信。 GPIO 控制器驱动程序调用由 GpioClx 实现的 [驱动程序支持方法](/previous-versions/hh439460(v=vs.85)) 。 GpioClx 调用由 GPIO 控制器驱动程序实现的 [事件回调函数](/previous-versions/hh439464(v=vs.85)) 。

GPIO 控制器驱动程序直接访问 GPIO 控制器设备的硬件寄存器。

GpioClx 处理来自物理连接到 GPIO pin 的外围设备的驱动程序的 i/o 请求。 GpioClx 将这些 i/o 请求转换为简单硬件操作，该操作通过调用由 GPIO 控制器驱动程序实现的事件回调函数来执行。 例如，若要从一组 GPIO pin 中读取数据或将数据写入到其中，GpioClx 将调用事件回调函数，例如 [*客户端 \_ ReadGpioPins*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins) 和 [*客户端 \_ WriteGpioPins*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins)。 GpioClx 管理 GPIO 控制器的 i/o 队列，从而免除了此任务的 GPIO 控制器驱动程序。

此外，GpioClx 还处理 GPIO 控制器设备的主中断，并将这些中断映射到辅助中断，由外围设备驱动程序处理。 主中断是硬件设备生成的中断。 辅助中断由操作系统生成，以响应特定的主中断。 主中断和辅助中断均由全局系统中断 (GSIs) 标识。 用于硬件平台的 ACPI 固件将 GSIs 分配给主中断，并且在运行时，操作系统将 GSIs 分配到辅助中断。

例如，固件会将 GSI 分配给 GPIO 控制器的硬件中断，操作系统会将 GSI 分配给配置为中断输入的 GPIO pin。

GpioClx 实现了一个 ISR，用于处理 GPIO 控制器设备的硬件生成的主中断。 当外围设备在 GPIO pin 上断言中断，并且此 pin 上的中断已启用且未屏蔽，GPIO 控制器将中断处理器。 作为响应，内核陷阱处理程序将 GpioClx ISR 计划为运行。 为了识别导致中断的 GPIO pin，GpioClx ISR 会调用由 GPIO 控制器驱动程序实现的 [*客户端 \_ QueryActiveInterrupts*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts) 事件回调函数。 然后，GpioClx ISR 查找分配给此 pin 的 GSI，并将此 GSI 传递到硬件抽象层 (HAL) 。 HAL 通过调用为此 GSI 注册的 ISR 来生成辅助中断。 此 ISR 属于最初断言中断的外围设备的驱动程序。

有关主要和次要中断的详细信息，请参阅 [GPIO 中断](./gpio-interrupts.md)。

## <a name="drivers-for-peripheral-devices-that-use-gpio-pins"></a>使用 GPIO Pin 的外围设备的驱动程序


在启动时，即插即用 (PnP) manager 将同时枚举 PnP 设备和非 PnP 设备。 对于已固定与 GPIO pin 的连接的非 PnP 设备，PnP 管理器会查询平台固件以确定哪些 GPIO pin 作为系统托管的硬件资源分配到这些设备。

外围设备的 KMDF 驱动程序在 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调期间接收其分配的硬件资源。 这些资源可能包括配置为数据输出、数据输入或中断请求输入的 GPIO pin。

GPIO i/o 资源是 Windows 8 中的一种新 Windows 资源类型。 此资源由一个或多个可用作数据输入或数据输出的 GPIO pin 集组成。 如果外设驱动程序为读取打开 GPIO i/o 资源，驱动程序将使用资源中的所有 pin 作为数据输入。 如果驱动程序为写入打开 GPIO i/o 资源，驱动程序将使用资源中的所有 pin 作为数据输出。 有关显示外围设备驱动程序如何与 GPIO i/o 引脚集建立逻辑连接的代码示例，请参阅以下主题：

[将 KMDF 驱动程序连接到 GPIO I/O 管脚](./connecting-a-kmdf-driver-to-gpio-i-o-pins.md)

配置为中断输入的 GPIO pin 将作为普通 Windows 中断资源分配给驱动程序。 中断资源抽象隐藏了一个事实，即一个中断可能由 GPIO pin 实现，而不是一个可编程中断控制器。 因此，驱动程序可以将基于 GPIO 的中断资源视为与其他任何中断资源相同。

若要访问 GPIO i/o 资源中的 GPIO pin，外围设备驱动程序必须打开与 pin 的逻辑连接。 KMDF 驱动程序调用 [**WdfIoTargetOpen**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen) 方法来打开连接。 通过此连接，驱动程序可以将 i/o 请求发送到 GPIO pin。 驱动程序会发送 [**IOCTL \_ gpio \_ 读取 \_ pin**](/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins) 请求，以从这些 pin 读取数据 (如果它们是输入插针) 或 [**IOCTL \_ gpio \_ 写入 \_ pin**](/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins) 请求写入数据 (如果它们是) 的输出插针。

若要从某个中断资源的 GPIO pin 接收中断，外围设备驱动程序必须将其中断服务例程注册 (ISR) ，以接收来自此 pin 实现的中断资源的中断。 KMDF 驱动程序调用 [**WdfInterruptCreate**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) 方法将 ISR 连接到中断。 

 

