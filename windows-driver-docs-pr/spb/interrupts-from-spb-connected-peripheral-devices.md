---
title: 来自 SPB 连接的外围设备的中断
description: 与不同的是如 PCI 总线，如 I²C 或 SPI，一个简单的外围总线 （存储） 提供了传达给处理器的中断请求从外围设备没有标准化的总线特定方法。
ms.assetid: E302BB21-582E-494E-9ADD-72703EF32446
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3166cc05a2950197a9375ba54f046562165294a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386297"
---
# <a name="interrupts-from-spb-connected-peripheral-devices"></a>来自 SPB 连接的外围设备的中断


与不同的是如 PCI 总线[简单的外围总线](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))（存储），如 I²C 或 SPI，标准化的不提供特定于总线的意味着要传达给处理器的中断请求从外围设备。 与之相反，通过 SPB 连接的外围设备通过单独的硬件路径来指示某个中断，该路径位于 SPB 和 SPB 控制器外部。 此中断路径的详细信息往往会因不同的硬件平台到下一步，但 Windows 会隐藏这些详细信息从存储连接外围设备，以便跨各种硬件平台工作的驱动程序的驱动程序。




通常情况下，中断请求行从与存储连接的外围设备连接到的常规用途的 I/O (GPIO) 控制器上的 pin 和 GPIO 控制器中继来自设备到处理器的中断。 有关详细信息，请参阅[GPIO 中断](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)。

外围设备驱动程序获取 GPIO 中断，用作 Windows 中断资源的抽象 (**CmResourceTypeInterrupt**)，并连接到驱动程序的中断服务例程 (ISR) 的中断。 中断资源抽象隐藏该驱动程序从中断的特定于平台的详细信息。 例如，驱动程序可以忽略详细信息，例如从 GPIO 插针或从其他来源是否收到中断。 若要保持这种抽象，内核的中断陷阱处理程序，它在 DIRQL 运行时，可能需要通过清除或暂时屏蔽在 GPIO pin 中断提示的活动中断请求。 GPIO 控制器的硬件寄存器通常是内存映射，并可以 DIRQL 上访问。

与此相反，与存储连接的外围设备不是内存映射，并为此设备 ISR 通常都必须运行在 IRQL = 被动\_级别。 若要访问的设备中的硬件寄存器，ISR 发送对存储执行串行传输的 I/O 请求。 此类传输相对较慢，且不能在运行在 DIRQL ISR 中执行。 但是，被动级别 ISR 可以同步发送的 I/O 请求，并一直阻止到该请求完成。

边缘触发中断，内核的陷阱处理程序自动清除处的 GPIO 是固定的中断请求，然后安排设备的 ISR 以被动级别运行。 陷阱处理程序必须清除以防止再次发生后的陷阱处理程序返回相同的中断的中断。

级别触发中断，内核的中断的陷阱处理程序自动掩盖了处的 GPIO 是固定的中断请求，然后安排设备的 ISR 以被动级别运行。 ISR 必须清除设备中的中断请求。 ISR 返回后，内核解除屏蔽在 GPIO pin 中断请求。

设备的被动级别 ISR 应执行仅限初始服务的中断，，然后返回以避免延迟被动级别 Isr 为其他设备。 通常情况下，该驱动程序应推迟到中断工作线程，其运行速度比 ISR 较低优先级的其他中断相关处理

从 Windows 8 开始[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)(UMDF) 支持 Isr UMDF 驱动程序。 存储外设的 UMDF 驱动程序调用[ **IWDFDevice3::CreateInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)方法以从设备连接到中断的 ISR。 当设备向发出信号的中断请求时，内核的陷阱处理程序计划 ISR 以被动级别运行。 有关详细信息，请参阅[访问硬件并处理中断](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-hardware-and-handling-interrupts)。

从 Windows 8 开始[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(KMDF) 支持被动级别 Isr。 存储外围设备的 KMDF 驱动程序调用[ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)方法以从设备连接到中断的被动级别 ISR。 此方法的输入参数之一是一个指向[ **WDF\_中断\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)结构，其中包含中断的配置信息。 若要配置 ISR 以被动级别运行，请设置**PassiveHandling**到此结构的成员**TRUE**。 有关详细信息，请参阅[支持被动级别中断](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-passive-level-interrupts)。

 

 




