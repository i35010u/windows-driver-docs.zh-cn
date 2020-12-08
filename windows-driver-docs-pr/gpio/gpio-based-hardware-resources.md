---
title: 基于 GPIO 的硬件资源
description: 从 Windows 8 开始，受 GPIO 控制器驱动程序控制的常规用途 I/O (GPIO) 引脚可以作为系统管理的硬件资源供其他驱动程序使用。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cd0eca3b5921690847a7b0804d3e0ff15069e70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830617"
---
# <a name="gpio-based-hardware-resources"></a>基于 GPIO 的硬件资源


从 Windows 8 开始，受 GPIO 控制器驱动程序控制的常规用途 I/O (GPIO) 引脚可以作为系统管理的硬件资源供其他驱动程序使用。 GPIO I/O 的引脚是已配置为数据输入或数据输出的引脚，可以作为新的 Windows 资源类型（即 *GPIO I/O 资源*）使用。 另外，GPIO 中断引脚是已配置为中断请求输入的引脚，可以作为普通 Windows 中断资源使用。

GPIO i/o 资源表示一个或多个 GPIO pin 的集合，外围设备的驱动程序可以对其进行读取或写入。 Windows 隐藏了有关 GPIO i/o 引脚基础实现的详细信息，以便可以编写外围设备驱动程序来操作抽象的 GPIO i/o 资源。 使用这些抽象资源的外围设备驱动程序可以跨平台工作，而不考虑实现资源的 GPIO 控制器硬件。 GPIO i/o 资源由 WDFIOTARGET 句柄表示，该句柄将此资源与拥有基础 GPIO pin 或 pin 的特定 GPIO 控制器驱动程序相关联。

通常，GPIO 控制器上的 i/o pin 可以配置为输入或输出，具体取决于控制器硬件和物理连接到 pin 的设备的功能。 因此，驱动程序可以为写入或读取操作打开到此 pin 的逻辑连接，但不能同时打开两者。 但是，此约束由硬件施加，而不由 GPIO 框架扩展 (GpioClx) 。 如果硬件启用了为输入和输出配置的 i/o pin，则 GpioClx 使驱动程序可以打开到 pin 的逻辑连接，以便进行读写操作。

对于配置为中断请求输入的 GPIO pin，操作系统会完全提取中断请求（而不是中断控制器或专用中断请求线路）来实现中断请求。 GPIO 中断将作为抽象中断资源提供给外围设备驱动程序。 GPIO 驱动程序堆栈和硬件抽象层都支持这些资源的抽象 (HAL) 。 因此，使用中断资源的外围设备驱动程序可以很大程度上忽略这些资源的基础实现的详细信息。 有关详细信息，请参阅 [GPIO 中断](./gpio-interrupts.md)。

下图显示了将基于 GPIO 的资源分配给两个外围设备驱动程序的示例：

![基于 gpio 的资源的分配示例](images/gpioresources.png)

在上图中，为以下三个基于 GPIO 的资源分配了外设驱动程序 A：

-   两个数据输入插针
-   数据输出插针
-   中断输入插针

以下两个基于 GPIO 的资源分配给外围设备驱动程序 B：

-   数据输入插针
-   中断输入插针

驱动程序 A 和 B 在其 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调函数中接收其已分配的资源。 如果驱动程序以资源的形式接收一个或多个 GPIO i/o 引脚集，则驱动程序可以打开到这些 pin 的连接来访问它们。 驱动程序获取 WDFIOTARGET 句柄来识别连接，并向此句柄发送 i/o 请求，以读取或写入这些 pin。

有关演示如何连接到一组 GPIO i/o 引脚并向此 pin 发送 i/o 请求的代码示例，请参阅以下主题：

[将 KMDF 驱动程序连接到 GPIO I/O 管脚](./connecting-a-kmdf-driver-to-gpio-i-o-pins.md)

在这两个主题中， `IoRoutine` 代码示例中的函数会打开用于读取或写入的 GPIO i/o pin 资源，具体取决于 `ReadOperation` 参数值。 如果打开资源以读取 (`DesiredAccess` = 泛型 \_ READ) ，则会将资源中的 pin 配置为输入，并向 pin 资源发送一项 [**IOCTL \_ GPIO \_ 读取 \_ pin**](/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins) 请求，以在这些 pin 读取输入值。 GpioClx 不允许向 [**IOCTL \_ gpio \_ 写入 \_ pin**](/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins) 请求发送一组输入插针，并完成此类请求，状态为 \_ GPIO \_ 操作 \_ 被拒绝。 同样，如果打开 pin 资源来写入 (`DesiredAccess` = 一般 \_ 写入) ，则会将资源中的 pin 配置为输出，并将 **IOCTL \_ GPIO \_ 写入 \_** pin 请求发送到 pin 资源会设置驱动这些 pin 的输出闩锁中的值。 通常，将 **IOCTL \_ GPIO \_ 读取 \_ pin** 请求发送到一组输出插针只会读取写入到输出闩锁的最后一个值。

若要使用中断资源接收中断，客户端驱动程序必须将 (ISR) 的中断服务例程连接到中断。 通常，驱动程序会通过调用 [**WdfInterruptCreate**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) 方法来建立此连接， (或 [**IoConnectInterruptEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex) 例程) 。 有关 KMDF 中断的详细信息，请参阅 [创建中断对象](../wdf/creating-an-interrupt-object.md)。

与可动态连接到硬件平台并从其断开连接即插即用设备相反，GPIO 控制器设备是永久性的。 此外，使用 GPIO 引脚和外围设备之间的连接被认为是永久性的。  (或者，如果可以从插槽中拔出外围设备，则该插槽专用于此设备。 ) 因此，可用的 GPIO 资源是固定的，可以在平台固件中指定。 同样，使用 GPIO 资源的外围设备驱动程序被认为是使用特定的 GPIO 资源集。 因此，可以在平台固件中指定这些设备驱动程序的资源要求。

当平台固件将一组 GPIO pin 指定为 GPIO i/o 资源时，固件会指示是否可以为读取、写入或读取和写入打开此资源中的 pin。

如果外围设备驱动程序使用多个 GPIO i/o 资源，则此驱动程序必须知道 PnP 管理器枚举这些资源的顺序。 例如，如果驱动程序使用两个 GPIO i/o 引脚，但必须独立地单独访问这些 pin，则平台固件应将每个 pin 描述为单独的 GPIO i/o 资源。 PnP 管理器按平台固件中描述的顺序枚举这些资源，这些资源必须符合驱动程序所需的顺序。

在外围设备驱动程序打开与 GPIO i/o 资源的连接后，该驱动程序发送到此连接的 [**ioctl \_ gpio \_ 读取 \_ pin**](/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins) 或 [**ioctl \_ gpio \_ 写入 \_ pin**](/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins) 请求将访问资源中的所有 pin。 如果驱动程序有时必须仅访问这些 pin 的子集，则必须将此子集作为单独的资源分配给驱动程序。

有关 **ioctl \_ gpio \_ 读取 \_ pin** 请求的详细信息，包括将数据输入插针映射到请求输出缓冲区中的位的详细信息，请参阅 [**IOCTL \_ GPIO \_ 读取 \_ pin**](/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)。 有关 **ioctl \_ gpio \_ 写入 \_ pin** 请求的详细信息，包括请求输入缓冲区中的位映射到数据输出插针的详细信息，请参阅 [**IOCTL \_ gpio \_ 写入 \_ pin**](/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins)。

 

