---
title: 来自 SPB 连接的外围设备的中断
description: 与 PCI （如 PCI）不同，简单的外围总线 (SPB) （例如，i2c 或 SPI）不提供标准化的、特定于总线的方式来将中断请求传达给处理器。
ms.assetid: E302BB21-582E-494E-9ADD-72703EF32446
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06d7f72cb220af57a831710d8b483348b3be685a
ms.sourcegitcommit: c766ab74e32eb44795cbbd1a4f352d3a6a9adc14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89389563"
---
# <a name="interrupts-from-spb-connected-peripheral-devices"></a>来自 SPB 连接的外围设备的中断


与 PCI （如 PCI）不同， [简单的外围总线](/previous-versions/hh450903(v=vs.85)) (SPB) （例如，I2C 或 SPI）不提供标准化的、特定于总线的方式来将中断请求传达给处理器。 与之相反，通过 SPB 连接的外围设备通过单独的硬件路径来指示某个中断，该路径位于 SPB 和 SPB 控制器外部。 此中断路径的详细信息与下一个硬件平台不同，但 Windows 将从与 SPB 连接的外围设备的驱动程序中隐藏这些详细信息，以使驱动程序能够在各种硬件平台上工作。




通常，来自已连接到 SPB 的外围设备的中断请求线路连接到常规用途 i/o (GPIO) 控制器上的 pin，GPIO 控制器会将从设备到处理器的中断中继。 有关详细信息，请参阅 [GPIO 中断](../gpio/gpio-interrupts.md)。

外围设备驱动程序将此 GPIO 中断获取为抽象的 Windows 中断资源 (**CmResourceTypeInterrupt**) 并将中断连接到驱动程序的中断服务例程 (ISR) 。 中断资源抽象将从驱动程序中隐藏特定于平台的中断的详细信息。 例如，驱动程序可能会忽略详细信息，例如是否从 GPIO pin 或其他某个源接收中断。 若要维护此抽象，内核中断陷阱处理程序（在 DIRQL 上运行）可能需要通过清除或临时屏蔽 GPIO pin 中断来使活动中断请求无提示。 GPIO 控制器的硬件寄存器通常是内存映射的，可以在 DIRQL 访问。

与此相反，与 SPB 连接的外围设备不会进行内存映射，并且此设备的 ISR 通常必须在 IRQL = 被动 \_ 级别运行。 为了访问设备中的硬件寄存器，ISR 发送了 i/o 请求，以通过 SPB 执行串行传输。 此类传输相对较慢，无法在 DIRQL 上运行的 ISR 中执行。 但是，被动级 ISR 可以同步发送 i/o 请求，然后在请求完成前阻止。

对于边缘触发的中断，内核的陷阱处理程序会在 GPIO pin 处自动清除中断请求，然后将设备的 ISR 计划为在被动级别运行。 陷阱处理程序必须清除中断，以防在陷阱处理程序返回之后再次出现同一中断。

对于级别触发的中断，内核的中断陷阱处理程序会在 GPIO pin 处自动屏蔽中断请求，然后将设备的 ISR 计划为在被动级别运行。 ISR 必须从设备清除中断请求。 ISR 返回后，内核会在 GPIO pin 解除中断请求。

设备的被动级别 ISR 只应执行中断的初始维护，然后返回以避免为其他设备延迟被动级别的 Isr。 通常，驱动程序应将与中断相关的其他处理延迟为中断工作线程，该线程的运行优先级低于 ISR。

从 Windows 8 开始， [用户模式驱动程序框架](../wdf/overview-of-the-umdf.md) (umdf) 支持用于 umdf 驱动程序的 isr。 用于 SPB 外围设备的 UMDF 驱动程序会调用 [**IWDFDevice3：： CreateInterrupt**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt) 方法，将 ISR 连接到设备上的中断。 当设备通知中断请求时，内核的陷阱处理程序会将 ISR 计划为在被动级别运行。 有关详细信息，请参阅 [访问硬件和处理中断](../wdf/accessing-hardware-and-handling-interrupts.md)。

从 Windows 8 开始， [内核模式驱动程序框架](../wdf/index.md) (KMDF) 支持被动级 isr。 用于 SPB 外围设备的 KMDF 驱动程序调用 [**WdfInterruptCreate**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) 方法，将被动级别 ISR 连接到设备中断。 此方法的输入参数之一是指向 [**WDF \_ 中断 \_ CONFIG**](/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config) 结构的指针，该结构包含中断的配置信息。 若要将 ISR 配置为在被动级别运行，请将此结构的 **PassiveHandling** 成员设置为 **TRUE**。 有关详细信息，请参阅 [支持被动级别中断](../wdf/supporting-passive-level-interrupts.md)。

 

