---
title: 与中断相关的回调
description: 作为一个选项，用于常规用途 i/o (GPIO) 控制器的驱动程序可以为 GPIO 中断提供支持。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 097ec3dfc20973fccf30719d0c6c51f5e5d35484
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801785"
---
# <a name="interrupt-related-callbacks"></a>与中断相关的回调


作为一个选项，用于常规用途 i/o (GPIO) 控制器的驱动程序可以为 GPIO 中断提供支持。 为了支持 GPIO 中断，GPIO 控制器驱动程序实现了一组回调函数以管理这些中断。 驱动程序包含指向注册数据包中的这些回调函数的指针，驱动程序将自身注册为 GPIO framework 扩展 (GpioClx) 的客户端。 有关此注册数据包的详细信息，请参阅 [**GPIO \_ 客户端 \_ 注册 \_ 包**](/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_gpio_client_registration_packet)。

作为一种规则，作为芯片 (SoC) 芯片上的系统集成部件的 GPIO 控制器具有内存映射的硬件寄存器，可由 SoC 芯片中的处理器直接访问。 不过，单独的 GPIO 控制器设备可能通过串行总线从外部连接到 SoC 芯片，如下图所示。

![集成的 gpio 控制器和外部 gpio 控制器](images/gpioconnects.png)

在此图中，外部 GPIO 控制器连接到 I i2c 总线。 此总线由作为 SoC 芯片集成部分的 i2c 总线控制器控制。 外部 GPIO 控制器的中断请求线路连接到集成 GPIO 控制器上的 pin。 在此示例中， [GPIOCLX DDI](./gpioclx-ddi.md) 可以同时容纳集成的 gpio 控制器和外部 gpio 控制器。

如果 GPIO 控制器设备是内存映射设备，GPIO 控制器驱动程序可以直接访问 DIRQL 上控制器的硬件寄存器。 但是，如果使用串行控制器进行串行连接，GPIO 控制器驱动程序只能以 IRQL = 被动级别访问硬件寄存器 \_ ，如 [被动级别 isr](./passive-level-isrs.md)中所述。

具有内存映射硬件注册的 GPIO 控制器的驱动程序应将驱动程序提供的设备信息中的 **MemoryMappedController** 标志位设置为 GpioClx。 否则，GpioClx 假设硬件寄存器未进行内存映射，并且驱动程序只能访问以下寄存器： IRQL = 被动 \_ 级别。 有关此标志位的详细信息，请参阅 [**控制器 \_ 属性 \_ 标志**](/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_controller_attribute_flags)。

GpioClx 实现 (ISR) 服务中断请求的中断服务例程。 此 ISR 调用以下与中断相关的回调函数：

[*客户端 \_ClearActiveInterrupts*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts) 
 [*client \_ MaskInterrupts*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_mask_interrupts) 
 [*client \_ QueryActiveInterrupts*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts) 
 [*client \_ QueryEnabledInterrupts*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts) 
 [*client \_ UnmaskInterrupt*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)这些函数是在 DIRQL 或被动级别调用的 \_ ，具体取决于 GpioClx 中的 ISR 是在 DIRQL 还是被动 \_ 级别运行。 如果 **MemoryMappedController** = 1，则 ISR 会在 DIRQL 中调用这些函数， \_ 如果 **MemoryMappedController** = 0，则在被动级别调用这些函数。 在这两种情况下，ISR 会自动序列化其回调，以便调用其中一个函数不会在调用这些函数的另一个过程中发生。

仅在被动级别调用以下与中断相关的回调函数 \_ ，无论是否设置了 **MemoryMappedController** 标志：

[*客户端 \_DisableInterrupt*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt) 
 [*客户端 \_ EnableInterrupt*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)如果未设置 **MemoryMappedController** 标志，则在被动级别调用所有与中断相关的回调函数 \_ 。 GpioClx 会自动序列化对这些函数的调用，以便在调用这些函数中的另一个函数时不会发生对其中某个函数的调用。

但是，如果设置了 **MemoryMappedController** 标志，则 *客户端 \_ EnableInterrupt* 和 *客户端 \_ DisableInterrupt* 函数必须将其中断启用和禁用操作显式同步到 GpioClx ISR，后者会在 DIRQL 调用其他四个中断相关的回调函数。

通常，其他 <em>客户端 \_</em>Xxx 回调函数 (其名称不包含 "*中断*" ) 不会执行与中断相关的处理，因此不需要同步到 GpioClx ISR。 但是，如果在被动级别调用了这些函数中的任何一种， \_ 并且包含访问中断设置（在 DIRQL 中由中断相关函数访问）的代码，则必须将此代码同步到 ISR。

为了支持中断同步，GpioClx 实现了一组中断锁。 在被动级别运行的回调函数 \_ 可以调用 [**gpio \_ CLX \_ AcquireInterruptLock**](/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock) 方法来获取中断锁，并调用 [**gpio \_ CLX \_ ReleaseInterruptLock**](/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock) 方法来释放该锁。 当函数包含中断锁时，GpioClx ISR 无法运行，并且此 ISR 无法调用任何中断相关的回调函数。 为了能够及时处理 GPIO 中断，驱动程序应保持中断锁，使其不再是必需的。

有关详细信息，请参阅 [GPIO 控制器驱动程序的中断同步](./interrupt-synchronization-for-gpio-controller-drivers.md)。

 

