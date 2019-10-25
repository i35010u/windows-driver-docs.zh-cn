---
title: 基于 GPIO 的硬件资源
description: 从 Windows 8 开始，受 GPIO 控制器驱动程序控制的常规用途 I/O (GPIO) 引脚可以作为系统管理的硬件资源供其他驱动程序使用。
ms.assetid: 03A6ACDF-8BB7-40C0-A331-7F61F48A44DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdccf2d2748cc9d912f99d396e32d77031381ca5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825049"
---
# <a name="gpio-based-hardware-resources"></a>基于 GPIO 的硬件资源


从 Windows 8 开始，受 GPIO 控制器驱动程序控制的常规用途 I/O (GPIO) 引脚可以作为系统管理的硬件资源供其他驱动程序使用。 GPIO I/O 的引脚是已配置为数据输入或数据输出的引脚，可以作为新的 Windows 资源类型（即 *GPIO I/O 资源*）使用。 另外，GPIO 中断引脚是已配置为中断请求输入的引脚，可以作为普通 Windows 中断资源使用。

GPIO i/o 资源表示一个或多个 GPIO pin 的集合，外围设备的驱动程序可以对其进行读取或写入。 Windows 隐藏了有关 GPIO i/o 引脚基础实现的详细信息，以便可以编写外围设备驱动程序来操作抽象的 GPIO i/o 资源。 使用这些抽象资源的外围设备驱动程序可以跨平台工作，而不考虑实现资源的 GPIO 控制器硬件。 GPIO i/o 资源由 WDFIOTARGET 句柄表示，该句柄将此资源与拥有基础 GPIO pin 或 pin 的特定 GPIO 控制器驱动程序相关联。

通常，GPIO 控制器上的 i/o pin 可以配置为输入或输出，具体取决于控制器硬件和物理连接到 pin 的设备的功能。 因此，驱动程序可以为写入或读取操作打开到此 pin 的逻辑连接，但不能同时打开两者。 但是，此约束是由硬件（而非 GPIO 框架扩展（GpioClx））施加的。 如果硬件启用了为输入和输出配置的 i/o pin，则 GpioClx 使驱动程序可以打开到 pin 的逻辑连接，以便进行读写操作。

对于配置为中断请求输入的 GPIO pin，操作系统会完全提取中断请求（而不是中断控制器或专用中断请求线路）来实现中断请求。 GPIO 中断将作为抽象中断资源提供给外围设备驱动程序。 GPIO 驱动程序堆栈和硬件抽象层（HAL）支持这些资源的抽象。 因此，使用中断资源的外围设备驱动程序可以很大程度上忽略这些资源的基础实现的详细信息。 有关详细信息，请参阅[GPIO 中断](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)。

下图显示了将基于 GPIO 的资源分配给两个外围设备驱动程序的示例：

![基于 gpio 的资源的分配示例](images/gpioresources.png)

在上图中，为以下三个基于 GPIO 的资源分配了外设驱动程序 A：

-   两个数据输入插针
-   数据输出插针
-   中断输入插针

以下两个基于 GPIO 的资源分配给外围设备驱动程序 B：

-   数据输入插针
-   中断输入插针

驱动程序 A 和 B 在其[*EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数中接收其已分配的资源。 如果驱动程序以资源的形式接收一个或多个 GPIO i/o 引脚集，则驱动程序可以打开到这些 pin 的连接来访问它们。 驱动程序获取 WDFIOTARGET 句柄来识别连接，并向此句柄发送 i/o 请求，以读取或写入这些 pin。

有关演示如何连接到一组 GPIO i/o 引脚并向此 pin 发送 i/o 请求的代码示例，请参阅以下主题：

[将 KMDF 驱动程序连接到 GPIO i/o 引脚](https://docs.microsoft.com/windows-hardware/drivers/gpio/connecting-a-kmdf-driver-to-gpio-i-o-pins)

在这两个主题中，代码示例中的 `IoRoutine` 函数将为读取或写入操作打开 GPIO i/o pin 资源，具体取决于 `ReadOperation` 参数值。 如果资源已打开以进行读取（`DesiredAccess` = 一般\_读取），则资源中的 pin 配置为输入，而[**IOCTL\_GPIO\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)发送到 pin 资源的\_pin 请求将读取这些 pin 的输入值。 GpioClx 不允许[**IOCTL\_GPIO\_写入\_pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins)请求发送一组输入插针，并完成此类请求，状态\_GPIO\_操作\_拒绝的错误状态。 同样，如果为写入（`DesiredAccess` = 一般\_写入）打开 pin 资源，则资源中的 pin 将配置为输出，而**IOCTL\_GPIO\_写入**发送到 pin 资源的\_pin 请求将设置驱动这些针脚的输出闩锁。 通常情况下， **\_GPIO 发送 IOCTL\_读取\_** 的输出插针请求仅读取写入到输出闩锁的最后一个值。

若要使用中断资源接收中断，客户端驱动程序必须将中断服务例程（ISR）连接到中断。 通常，驱动程序会通过调用[**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)方法（或可能为[**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)例程）进行此连接。 有关 KMDF 中断的详细信息，请参阅[创建中断对象](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-an-interrupt-object)。

与可动态连接到硬件平台并从其断开连接即插即用设备相反，GPIO 控制器设备是永久性的。 此外，使用 GPIO 引脚和外围设备之间的连接被认为是永久性的。 （或者，如果可以从插槽中拔出外围设备，则该插槽专用于此设备。）因此，可用的 GPIO 资源是固定的，可以在平台固件中指定。 同样，使用 GPIO 资源的外围设备驱动程序被认为是使用特定的 GPIO 资源集。 因此，可以在平台固件中指定这些设备驱动程序的资源要求。

当平台固件将一组 GPIO pin 指定为 GPIO i/o 资源时，固件会指示是否可以为读取、写入或读取和写入打开此资源中的 pin。

如果外围设备驱动程序使用多个 GPIO i/o 资源，则此驱动程序必须知道 PnP 管理器枚举这些资源的顺序。 例如，如果驱动程序使用两个 GPIO i/o 引脚，但必须独立地单独访问这些 pin，则平台固件应将每个 pin 描述为单独的 GPIO i/o 资源。 PnP 管理器按平台固件中描述的顺序枚举这些资源，这些资源必须符合驱动程序所需的顺序。

在外围设备驱动程序打开与 GPIO i/o 资源的连接后， [**IOCTL\_gpio\_读取\_的 pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)或[**ioctl\_GPIO\_写入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins)此驱动程序发送到此连接访问的请求\_资源中的所有 pin。 如果驱动程序有时必须仅访问这些 pin 的子集，则必须将此子集作为单独的资源分配给驱动程序。

有关**IOCTL\_GPIO 的详细信息\_读取\_插**针请求，包括将数据输入插针映射到请求输出缓冲区中的位，请参阅[**IOCTL\_GPIO\_读取\_的 pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)。 若要详细了解**IOCTL\_GPIO\_写入\_pin**请求，包括请求输入缓冲区中的位映射到数据输出插针，请参阅[**IOCTL\_GPIO\_写入\_pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins)。

 

 




