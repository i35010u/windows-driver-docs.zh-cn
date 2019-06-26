---
title: 与中断相关的回调
description: 作为一个选项，常规用途的 I/O (GPIO) 控制器的驱动程序可以为 GPIO 中断提供支持。
ms.assetid: 638B52A0-CB8D-4A79-B7D1-ED2474E46DAE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4260c1ce47ee9d560b3a3c6a985b023995ee4959
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363573"
---
# <a name="interrupt-related-callbacks"></a>与中断相关的回调


作为一个选项，常规用途的 I/O (GPIO) 控制器的驱动程序可以为 GPIO 中断提供支持。 若要支持 GPIO 中断，GPIO 控制器驱动程序实现了一组回调函数来管理这些中断。 该驱动程序在驱动程序提供时它将自身注册为 GPIO 框架扩展 (GpioClx) 的客户端的注册数据包中包含指向这些回调函数的指针。 有关此注册包的详细信息，请参阅[ **GPIO\_客户端\_注册\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_gpio_client_registration_packet)。

一般来说，芯片 (SoC) 片上系统的集成部分 GPIO 控制器都有可直接访问通过 SoC 芯片中的处理器的内存映射硬件寄存器。 但是，单独的 GPIO 控制器设备可能是从外部连接到通过串行总线 SoC 芯片，如下图中所示。

![集成的 gpio 控制器和一个外部 gpio 控制器](images/gpioconnects.png)

在此图中，外部 GPIO 控制器连接到 I²C 总线。 此总线由 SoC 芯片的集成部分 I²C 总线控制器控制。 中断请求行从外部 GPIO 控制器连接到集成的 GPIO 控制器上的 pin。 [GpioClx DDI](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpioclx-ddi)集成的 GPIO 控制器和外部的 GPIO 控制器，在此示例中可以容纳。

如果 GPIO 控制器设备内存映射，GPIO 控制器驱动程序可以直接访问在 DIRQL 控制器的硬件寄存器。 但是，如果按顺序连接 GPIO 控制器，GPIO 控制器驱动程序可以访问仅在 IRQL 硬件寄存器 = 被动\_级别，如中所述[被动级别 Isr](https://docs.microsoft.com/windows-hardware/drivers/gpio/passive-level-isrs)。

该驱动程序应设置具有内存映射硬件的 GPIO 控制器注册**MemoryMappedController**标志位驱动程序提供对 GpioClx 的设备信息中。 否则，GpioClx 假定硬件寄存器不是内存映射，该驱动程序可以访问这些注册只能在 IRQL = 被动\_级别。 有关此标志位的详细信息，请参阅[**控制器\_特性\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_controller_attribute_flags)。

GpioClx 从 GPIO 控制器实现为请求提供服务中断的中断服务例程 (ISR)。 此 ISR 调用以下与中断相关的回调函数：

[*客户端\_ClearActiveInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)
[*客户端\_MaskInterrupts* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_mask_interrupts) 
 [ *客户端\_QueryActiveInterrupts*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts)
[*客户端\_QueryEnabledInterrupts* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts) 
[*客户端\_UnmaskInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt) DIRQL 或被动调用这些函数\_级别，具体取决于是否在 DIRQL 运行中 GpioClx ISR 或被动\_级别。 ISR 调用这些函数在 DIRQL 如果**MemoryMappedController** = 1，而在被动\_级别 if **MemoryMappedController** = 0。 在任一情况下，ISR 自动序列化其回调，以便对这些函数之一的调用不会调用这些函数的另一中间发生。

GPIO 框架扩展调用以下与中断相关的回调函数仅在被动\_级别，而不管是否**MemoryMappedController** 设置标志：

[*客户端\_DisableInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_disable_interrupt)
[*客户端\_EnableInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_enable_interrupt)如果**MemoryMappedController**未设置标志，所有与中断相关的回调函数以被动调用\_级别。 GpioClx 自动序列化对这些函数的调用，以便对这些函数之一的调用不会调用这些函数的另一中间发生。

但是，如果**MemoryMappedController**设置标志，则*客户端\_EnableInterrupt*并*客户端\_DisableInterrupt*函数必须显式同步其中断启用和禁用 GpioClx ISR，后者在 DIRQL 调用其他四个与中断相关的回调函数的操作。

通常情况下，另<em>客户端\_</em>Xxx 回调函数 (其名称不包含"*中断*") 不会进行与中断相关处理，并因此，不需要同步到 GpioClx ISR 但是，如果任何这些函数在调用被动\_级别和包含用于访问由在 DIRQL 与中断相关的函数访问的中断设置代码，此代码必须同步到 ISR

若要支持中断同步，GpioClx 实现一系列中断锁。 在被动运行的回调函数\_级别可以调用[ **GPIO\_CLX\_AcquireInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)方法获取的中断锁，并调用[ **GPIO\_CLX\_ReleaseInterruptLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)方法才能释放锁。 在该函数包含中断锁，GpioClx ISR 不能运行，而且此 ISR 不能调用任何与中断相关的回调函数。 若要启用 GPIO 中断及时的方式处理，该驱动程序应保存的中断锁不再不必要。

有关详细信息，请参阅[GPIO 控制器驱动程序中断同步](https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-synchronization-for-gpio-controller-drivers)。

 

 




