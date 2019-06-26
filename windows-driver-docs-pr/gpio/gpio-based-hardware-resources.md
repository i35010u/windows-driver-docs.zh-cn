---
title: 基于 GPIO 的硬件资源
description: 从 Windows 8 开始，受 GPIO 控制器驱动程序控制的常规用途 I/O (GPIO) 引脚可以作为系统管理的硬件资源供其他驱动程序使用。
ms.assetid: 03A6ACDF-8BB7-40C0-A331-7F61F48A44DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8719a9e327495962682b592b8d13e813394b07c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363637"
---
# <a name="gpio-based-hardware-resources"></a>基于 GPIO 的硬件资源


从 Windows 8 开始，受 GPIO 控制器驱动程序控制的常规用途 I/O (GPIO) 引脚可以作为系统管理的硬件资源供其他驱动程序使用。 GPIO I/O 的引脚是已配置为数据输入或数据输出的引脚，可以作为新的 Windows 资源类型（即 *GPIO I/O 资源*）使用。 另外，GPIO 中断引脚是已配置为中断请求输入的引脚，可以作为普通 Windows 中断资源使用。

GPIO I/O 资源表示一系列一个或多个 GPIO 插针的外围设备的驱动程序可以读取或写入。 Windows 隐藏有关 GPIO I/O pin 的底层实现的详细信息，以便可以将外围设备驱动程序编写为操作抽象 GPIO I/O 资源。 使用这些抽象的资源的外围设备驱动程序可跨平台而不考虑实现资源 GPIO 控制器硬件。 GPIO I/O 资源表示通过将此资源与拥有基础的 GPIO 插针或 pin 的特定 GPIO 控制器驱动程序相关联的 WDFIOTARGET 句柄。

通常情况下，用于输入或输出，具体取决于控制器硬件和设备物理连接到的插针的功能，可以配置 GPIO 控制器上的 I/O pin。 因此，驱动程序可以打开用于写入或读取的操作，但不是能同时与此 pin 的逻辑连接。 但是，此限制是由硬件，而不是 GPIO 框架扩展 (GpioClx)。 如果硬件启用要配置的输入和输出一个 I/O 插针，GpioClx 使驱动程序即可打开 pin 的逻辑连接进行读取和写入操作。

对于配置为中断请求输入，这一事实的中断请求由 GPIO pin，而不是实现通过中断控制器或专用的中断请求行完全由操作系统抽象化的 GPIO 插针。 GPIO 中断到外围设备驱动程序显示为抽象中断资源。 GPIO 驱动程序堆栈和硬件抽象层 (HAL) 提供支持这些资源的抽象。 因此，外围设备驱动程序的使用中断资源很大程度上可以忽略有关这些资源的底层实现的详细信息。 有关详细信息，请参阅[GPIO 中断](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupts)。

下图显示了基于 GPIO 的资源添加到两个外围设备驱动程序的示例作业：

![gpio 基于资源的示例工作分配](images/gpioresources.png)

在上图中，以下三种基于 GPIO 的资源分配外围设备驱动程序答：

-   两个数据输入插针
-   数据输出插针
-   中断输入插针

以下两个基于 GPIO 的资源分配到外围设备驱动程序 b:

-   数据输入插针
-   中断输入插针

驱动程序 A 和 B 接收在其已分配的资源及其[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数。 如果驱动程序接收，为资源，一组的一个或多个 GPIO I/O pin，驱动程序可以打开这些插针，以对其进行访问的连接。 该驱动程序获取 WDFIOTARGET 句柄确定连接，并将 I/O 请求发送到此句柄以读取或写入这些引脚。

代码示例演示如何连接到的 GPIO I/O pin 的一组并将 I/O 请求发送到此 pin，请参阅以下主题：

[连接到 GPIO I/O 插针的 KMDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/gpio/connecting-a-kmdf-driver-to-gpio-i-o-pins)

在这两个主题中，`IoRoutine`代码示例中的函数将打开 GPIO I/O pin 资源读取或写入操作，具体取决于`ReadOperation`参数值。 如果该资源打开用于读取 (`DesiredAccess` = 泛型\_读取)，在资源 pin 配置为输入，和一个[ **IOCTL\_GPIO\_读取\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_read_pins)请求发送到 pin 资源读取这些引脚的输入的值。 不允许 GpioClx [ **IOCTL\_GPIO\_编写\_PIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_write_pins)请求要发送的一组输入 pin，并完成此类请求状态\_GPIO\_操作\_拒绝的错误状态。 同样，如果 pin 资源打开进行写入 (`DesiredAccess` = 泛型\_编写)，为输出，配置中资源的针**IOCTL\_GPIO\_编写\_PIN**请求发送到 pin 资源设置中的驱动器这些引脚输出闩锁的值。 通常情况下，发送**IOCTL\_GPIO\_读取\_PIN**请求到一组输出插针，只需读取写入到输出闩锁的最后一个值。

若要使用的中断资源接收中断，客户端驱动程序必须连接到中断的中断服务例程 (ISR)。 通常情况下，该驱动程序建立此连接是通过调用[ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)方法 (也可能是[ **IoConnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)例程)。 有关 KMDF 中断的详细信息，请参阅[创建中断对象](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-an-interrupt-object)。

与即插可以动态地连接到和从一种硬件平台断开连接的设备，相比 GPIO 控制器设备永久连接。 此外，假定 GPIO 插针和外围设备之间的连接是永久性的。 （或者，如果外围设备可以从一个槽拔出，槽专用于此设备。）因此，可用的 GPIO 资源固定的可以在平台固件中指定。 同样，假定使用 GPIO 资源的外围设备驱动程序使用专用的 GPIO 资源集。 因此，可以在平台固件中指定这些设备驱动程序的资源要求。

当平台固件将 GPIO 插针的一组指定为 GPIO I/O 资源时，固件指示为读取、 写入或读取和写入是否可以打开此资源中的针。

如果外围设备驱动程序使用多个 GPIO I/O 资源，此驱动程序必须注意的即插即用 manager 枚举这些资源的顺序。 例如，如果驱动程序将使用两个 GPIO I/O pin，但独立地在不同时间必须访问这些引脚，平台固件应作为单独的 GPIO I/O 资源描述每个 pin。 PnP 管理器枚举这些资源的顺序必须匹配所需的驱动程序的平台固件中介绍的顺序。

外围设备驱动程序打开与 GPIO I/O 资源的连接后[ **IOCTL\_GPIO\_读取\_PIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_read_pins)或[ **IOCTL\_GPIO\_编写\_PIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_write_pins)此驱动程序将发送到此连接的请求访问所有球瓶的资源中。 如果驱动程序有时必须访问这些引脚的一个子集，则此子集必须分配给该驱动程序中作为单独的资源。

有关详细信息**IOCTL\_GPIO\_读取\_PIN**请求，包括在请求输出缓冲区中的数据输入 pin 的位的映射，请参阅[ **IOCTL\_GPIO\_读取\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_read_pins)。 有关详细信息**IOCTL\_GPIO\_编写\_PIN**请求，包括数据输出插针，将请求输入缓冲区中的位的映射，请参阅[ **IOCTL\_GPIO\_编写\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpio/ni-gpio-ioctl_gpio_write_pins)。

 

 




