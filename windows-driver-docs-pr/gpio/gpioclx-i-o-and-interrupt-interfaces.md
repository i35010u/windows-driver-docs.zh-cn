---
title: GpioClx I/O 和中断接口
description: 通常情况下，GPIO 控制器的客户端是连接到 GPIO 引脚的外围设备的驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1494533ddfd868a9cf56ada8d36b5569a3858a67
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821499"
---
# <a name="gpioclx-io-and-interrupt-interfaces"></a>GpioClx I/O 和中断接口


通常情况下，GPIO 控制器的客户端是连接到 GPIO 引脚的外围设备的驱动程序。 这些驱动程序使用 GPIO 引脚作为低带宽数据通道、设备选择器输出和中断请求输入。 外围设备驱动程序打开到 GPIO 引脚的逻辑连接，这些引脚已配置为数据输入或输出。 它们使用这些连接将 I/O 请求发送到这些引脚。 另外，外围设备驱动程序可以通过逻辑方式将其中断服务例程连接到已配置为中断请求输入的 GPIO 引脚。

GPIO pin 是系统托管的硬件资源。 在外设驱动程序启动其设备之前，即插即用 (PnP) manager 向此驱动程序分配硬件资源列表。 此硬件资源列表可能包括：

-   GPIO i/o 资源。 此资源是配置为数据输入或数据输出的一个或多个 GPIO pin 集。 GPIO i/o 资源是一种从 Windows 8 开始的新 Windows 资源类型。
-   中断。 此中断资源可能作为 GPIO pin （配置为中断输入）来实现，但它可能是通过可编程中断控制器实现的，或者是处理器包上的专用中断端口。 硬件抽象层 (HAL) 中断抽象隐藏了这些实现细节，客户端驱动程序可以安全地忽略这些细节。

在外设驱动程序可以使用一组 GPIO pin 作为数据输入或输出之前，驱动程序必须打开与这些 pin 的逻辑连接。 例如， (KMDF) 驱动程序的 [内核模式驱动程序接口](../wdf/index.md) 获取用于标识连接的 WDFIOTARGET 句柄。 驱动程序使用此句柄将 i/o 请求发送到 pin。 具体而言，客户端驱动程序将发送 [**IOCTL \_ gpio \_ 写入 \_ pin**](/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins) 和 [**ioctl \_ gpio \_ 读取 \_ 插针**](/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins) i/o 控制请求，以将数据写入到输出插针，并从输入插针读取数据。 有关演示如何连接到一组 GPIO i/o pin 的代码示例，请参阅以下主题：

[将 KMDF 驱动程序连接到 GPIO I/O 管脚](./connecting-a-kmdf-driver-to-gpio-i-o-pins.md)

若要使用中断资源接收中断，外围设备驱动程序必须以逻辑方式将中断服务例程连接 (ISR) 到中断。 例如，内核模式驱动程序可以通过调用 [**WdfInterruptCreate**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) 方法或 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex) 例程建立此连接。 连接后，当外围设备向 GPIO pin 或中断控制器输入发出中断请求信号时，驱动程序的 ISR 将运行。 有关中断的详细信息，请参阅 [创建中断对象](../wdf/creating-an-interrupt-object.md)。

GPIO framework 扩展 (GpioClx) 管理其客户端外设驱动程序的 i/o 连接和中断连接。 PnP 管理器可能会在 GPIO 控制器设备上将不同的 GPIO pin 组分配给不同的客户端驱动程序。 其中一些 pin 配置为数据输入或输出，一些则配置为中断请求输入。

当客户端驱动程序收到中断请求或向 GPIO 引脚发送 i/o 请求时，GpioClx 将调用 GPIO 控制器驱动程序实现的事件回调函数。 这些回调访问 GPIO 控制器设备中的硬件寄存器。 通过这些函数调用，GpioClx 读取数据输入，写入数据输出，并通过查询、启用、屏蔽、清除等，并) 将配置为中断输入的 GPIO pin 来管理中断请求 (。

GpioClx 执行管理客户端打开的 i/o 和中断连接所需的所有处理。 GPIO 控制器驱动程序-通过将这些连接的管理委托给 GpioClx，仅负责访问 GPIO 控制器设备中的硬件寄存器的相对简单任务。 GPIO 控制器驱动程序无需知道进行特定访问的客户端驱动程序。

 

