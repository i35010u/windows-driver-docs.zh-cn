---
title: SPB 外围设备驱动程序
description: SPB 外围设备驱动程序控制连接到简单外设总线 (SPB) 的外围设备。
ms.assetid: 8352EBD9-D94C-4EC6-A17E-3A72DDE4C16C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ebfb8ee176dc6176ed6d581f9785d11229d4a6a
ms.sourcegitcommit: 56e531c6dffd4d7a11c4c2d8edd59f0e1ca8929d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2020
ms.locfileid: "92133961"
---
# <a name="spb-peripheral-device-drivers"></a>SPB 外围设备驱动程序


SPB 外围设备驱动程序控制连接到[简单外设总线](/previous-versions/hh450903(v=vs.85)) (SPB) 的外围设备。 此设备的硬件寄存器只能通过 SPB 使用。 若要从设备读取数据或向其写入数据，驱动程序必须将 I/O 请求发送到 SPB 控制器。 只有该控制器可以通过 SPB 启动将数据传输到设备或从设备传输数据的过程。

从 Windows 8 开始，Windows 为 [简单外围总线](/previous-versions/hh450903(v=vs.85)) 上的外围设备提供驱动程序支持 (SPBs) 。 SPBs （如 i2c 和 SPI）广泛用于连接到低速传感器设备，例如加速感应器、GPS 设备和电池级别的监视器。 本概述介绍了 SPB 外围设备驱动程序与其他系统组件的合作方式如何控制由 SPB 连接的外围设备。

可以构建 SPB 外围设备驱动程序，以使用 [用户模式驱动程序框架](../wdf/overview-of-the-umdf.md) (UMDF) 或 [内核模式驱动程序框架](../wdf/index.md) (KMDF) 。 有关开发 UMDF 驱动程序的详细信息，请参阅 [使用 umdf 入门](/previous-versions/ff554928(v=vs.85))。 有关开发 KMDF 驱动程序的详细信息，请参阅 [使用 Kernel-Mode Driver Framework 入门](../wdf/index.md)。

## <a name="device-configuration-information"></a>设备配置信息


SPB 连接的外围设备的硬件寄存器不是内存映射的。 仅可通过 SPB 控制器访问设备，该控制器通过 SPB 以串行方式将数据传入和传出设备。 若要执行 i/o 操作，则 SPB 外设驱动程序会将 i/o 请求发送到设备，而 SPB 控制器将执行完成这些请求所需的数据传输。 有关可发送到 SPBs 上的外围设备的 i/o 请求的详细信息，请参阅 [使用 SPB I/o 请求接口](./using-the-spb-i-o-request-interface.md)。

下图显示了一个示例硬件配置，其中的 SPB （在本例中为 I i2c 总线）将两个外围设备连接到芯片 (SoC) 模块上的系统。 外围设备位于 SoC 模块外部，并连接到模块上的四个 pin。 SoC 模块包含 (未显示的主处理器) ，以及 I i2c 控制器和一个 [常规用途 i/o](../gpio/gpio-driver-support-overview.md) (GPIO) 控制器。 处理器使用 I I C 控制器将数据与两个外围设备进行串行传输。 这些设备的中断请求线路连接到配置为中断输入的两个 GPIO pin。 当设备通知中断请求时，GPIO 控制器会将中断中继到处理器。

![用于 spb 外围设备的连接](images/spbconnects.png)

由于此示例中的 GPIO 控制器和 i2c 控制器已集成到 SoC 模块，因此它们的硬件寄存器为内存映射，并且可由处理器直接访问。 但是，处理器仅可以通过 i2c 控制器间接访问两个外围设备的硬件寄存器。

SPB 不是 [即插即用](../kernel/introduction-to-plug-and-play.md) (PnP) 总线，因此不能用于自动检测和配置插入到总线中的新设备。 与 SPB 连接的设备的总线和中断连接通常是永久性的。 即使设备可以从插槽中拔出，此插槽通常专用于设备。 此外，SPB 不提供带内硬件路径，用于中继从总线上的外围设备到总线控制器的中断请求。 相反，中断的硬件路径与总线控制器分离。

硬件平台供应商在平台的 ACPI 固件中存储与 SPB 连接的外围设备的配置信息。 在系统启动期间， [ACPI 驱动程序](../acpi/enumerating-child-devices-and-control-methods.md) 会在总线上枚举 PnP 管理器的设备。 对于每个枚举设备，ACPI 提供有关设备总线和中断连接的信息。 PnP 管理器将此信息存储在名为 *资源中心*的数据存储中。

设备启动时，PnP 管理器会为设备驱动程序提供一组 [硬件资源](../kernel/hardware-resources.md) ，这些资源封装了资源中心为设备存储的配置信息。 这些资源包括连接 ID 和中断号。 连接 ID 封装了总线连接信息，如 SPB 控制器、总线地址和总线时钟频率。 在将 i/o 请求发送到设备之前，驱动程序必须先使用连接 ID 打开与设备的逻辑连接。 中断号是一个 Windows 中断资源，驱动程序可将其中断服务例程连接 (ISR) 。 可以轻松地将驱动程序从一个硬件平台移植到另一个硬件平台，因为连接 ID 和中断号是用于隐藏有关物理总线和中断连接的特定于平台的信息的高级抽象。

## <a name="software-and-hardware-layers"></a>软件和硬件层


以下块示意图显示了将 SPB 上的外围设备连接到使用该设备的应用程序的软件和硬件层。 此示例中的 "SPB 外围设备驱动程序" 是一个 UMDF 驱动程序。 图底部的外围设备 () 是传感器设备 (例如，加速感应器) 。 如前面的关系图中所示，外围设备连接到 I i2c 总线，并通过 GPIO 控制器上的 pin 发出中断请求信号。

![与 spb 连接的传感器设备的软件和硬件层](images/spblayers.png)

以灰色显示的三个块是系统提供的模块。 从 Windows 7 开始，可以将 [传感器类扩展](../sensors/about-the-sensor-class-extension.md) 用作 UMDF 的传感器特定扩展。 从 Windows 8 开始， [SPB 框架扩展](./spb-framework-extension.md) (SpbCx) 和 [gpio Framework 扩展](../gpio/gpio-driver-support-overview.md) (GPIOCLX) 可作为 KMDF 扩展，这些扩展执行特定于 SPB 控制器和 gpio 控制器的功能。

在上述关系图的顶部，应用程序调用 [传感器 API](/windows/desktop/SensorsAPI/portal) 或 [位置 API](/windows/desktop/LocationAPI/windows-location-api-portal) 中的方法来与传感器设备通信。 通过这些调用，应用程序可以将 i/o 请求发送到设备，并从设备接收事件通知。 有关这些 Api 的详细信息，请参阅 [Windows 中的传感器和位置平台简介](../sensors/index.md)。

当应用程序调用需要与 SPB 外围设备驱动程序通信的方法时，传感器 API 或位置 API 会创建 i/o 请求并将其发送到 SPB 外围设备驱动程序。 传感器类扩展模块有助于驱动程序处理这些 i/o 请求。 当驱动程序收到新的 i/o 请求时，驱动程序会立即将请求传递给传感器类扩展，这会将请求排队，直到驱动程序准备好处理该请求。 如果从应用程序发出的 i/o 请求需要将数据传输到外设或从外围设备传输数据，则 SPB 外围设备驱动程序将为此传输创建 i/o 请求，并将请求发送到 I i2c 控制器。 此类请求由 SpbCx 和 I i2c 控制器驱动程序共同处理。

SpbCx 是系统提供的组件，用于管理 SPB 控制器的 i/o 请求队列，如本示例中的 i2c 控制器。 由控制器的硬件供应商提供的 I-C 控制器驱动程序管理 I i2c 控制器中所有特定于硬件的操作。 例如，控制器驱动程序可访问控制器的内存映射硬件寄存器，以启动到外部设备的数据传输并通过 I i2c 总线传输。

当发生硬件事件，需要从 SPB 外围设备驱动程序或用户模式应用程序中注意时，外围设备会发出中断请求的信号。 外围设备的中断线路连接到配置为接收中断请求的 GPIO pin。 当设备向 GPIO pin 发出信号时，GPIO 控制器会将中断通知给处理器。 为响应此中断，内核的中断陷阱处理程序会调用 GpioClx 的 ISR。 此 ISR 会查询 GPIO 控制器驱动程序，然后访问 GPIO 控制器的内存映射硬件寄存器来识别中断的 GPIO pin。 若要静默中断，GPIO 控制器驱动程序会清除 (如果中断是边缘触发的) 或屏蔽 (如果级别触发的) 在 GPIO pin 中断请求。 中断必须静默，以防止处理器在陷阱处理程序返回时再次采用相同的中断。 对于级别触发的中断，SPB 外围设备驱动程序中的 ISR 必须访问外围设备的硬件寄存器，才能在 GPIO 锁定之前清除中断。

内核的中断陷阱处理程序返回之前，会将 SPB 外围设备驱动程序中的 ISR 计划为以 IRQL = 被动 \_ 级别运行。 从 Windows 8 开始，UMDF 驱动程序可以将其 ISR 连接到驱动程序作为抽象 Windows 中断资源接收的中断;有关详细信息，请参阅 [处理中断](../wdf/handling-interrupts.md)。 为了确定要调用哪个 ISR，操作系统会查找分配给中断的 GPIO pin 的虚拟中断，并找到连接到中断的 ISR。 此虚拟中断在上图中标记为 *辅助* 中断。 与此相反，GPIO 控制器的硬件中断标记 *为主* 中断。

由于 SPB 外围设备驱动程序中的 ISR 在被动级别运行，因此 ISR 可以使用同步 i/o 请求来访问外围设备中的硬件寄存器。 ISR 可以在这些请求完成之前一直阻止。 以相对较高的优先级运行的 ISR 应该尽快返回，并将中断的所有后台处理推迟到以较低优先级运行的辅助进程。

为响应辅助中断，SPB 外围设备驱动程序会在传感器类扩展中发布事件，该扩展通过传感器 API 或位置 API 通知事件的用户模式应用程序。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/spb/using-the-spb-i-o-request-interface" data-raw-source="[Using the SPB I/O Request Interface](./using-the-spb-i-o-request-interface.md)">使用 SPB I/O 请求接口</a></p></td>
<td><p>从 Windows 8 开始， <a href="/windows-hardware/drivers/spb/spb-framework-extension" data-raw-source="[SPB framework extension](./spb-framework-extension.md)">SPB framework 扩展</a> (SpbCx) 是系统提供的组件，它支持 <a href="/previous-versions/hh698224(v=vs.85)" data-raw-source="[SPB I/O request interface](/previous-versions/hh698224(v=vs.85))">SPB i/o 请求接口</a>。 SPB 外围设备驱动程序使用此接口将 i/o 请求发送到连接到 i2c、SPI 和其他 <a href="/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral buses](/previous-versions/hh450903(v=vs.85))">简单外围总线</a> 的设备， (SPBs) 。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices" data-raw-source="[Connection IDs for SPB-Connected Peripheral Devices](./connection-ids-for-spb-connected-peripheral-devices.md)">SPB 连接的外围设备的连接 ID</a></p></td>
<td><p>驱动程序可以将 i/o 请求发送到 <a href="/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](/previous-versions/hh450903(v=vs.85))">简单外围总线</a> 上的外围设备 (SPB) 中，驱动程序必须打开与设备的逻辑连接。 通过此连接，驱动程序可以发送读写请求，以便将数据传入和传出设备。 此外，驱动程序可以将 (IOCTL) 请求的 i/o 控制发送到设备，以便执行特定于 SPB 的操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/spb/spb-device-stacks" data-raw-source="[SPB Device Stacks](./spb-device-stacks.md)">SPB 设备堆栈</a></p></td>
<td><p>Windows 驱动模型完全分离了用于控制外围设备的驱动程序组件 (例如，从管理总线控制器的驱动程序组件的总线上的温度传感器) ，后者可在外围设备之间传输数据和控制信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/spb/interrupts-from-spb-connected-peripheral-devices" data-raw-source="[Interrupts from SPB-Connected Peripheral Devices](./interrupts-from-spb-connected-peripheral-devices.md)">来自 SPB 连接的外围设备的中断</a></p></td>
<td><p>与 PCI （如 PCI）不同， <a href="/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](/previous-versions/hh450903(v=vs.85))">简单的外围总线</a> (SPB) （例如，I2C 或 SPI）不提供标准化的、特定于总线的方式来将中断请求传达给处理器。 与之相反，通过 SPB 连接的外围设备通过单独的硬件路径来指示某个中断，该路径位于 SPB 和 SPB 控制器外部。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/spb/hardware-resources-for-kernel-mode-spb-peripheral-drivers" data-raw-source="[Hardware Resources for Kernel-Mode SPB Peripheral Drivers](./hardware-resources-for-kernel-mode-spb-peripheral-drivers.md)">内核模式 SPB 外设驱动程序的硬件资源</a></p></td>
<td><p>本主题中的代码示例演示如何将 <a href="/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers" data-raw-source="[Kernel-Mode Driver Framework](../wdf/index.md)">内核模式驱动程序框架</a> (KMDF) 驱动程序安装到 <a href="/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](/previous-versions/hh450903(v=vs.85))">简单外围总线</a> (SPB 上，) 如何获取操作设备所需的硬件资源。 这些资源包含驱动程序用于建立到设备的逻辑连接的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/spb/hardware-resources-for-user-mode-spb-peripheral-drivers" data-raw-source="[Hardware Resources for User-Mode SPB Peripheral Drivers](./hardware-resources-for-user-mode-spb-peripheral-drivers.md)">用户模式 SPB 外设驱动程序的硬件资源</a></p></td>
<td><p>本主题中的代码示例演示了在<a href="/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](/previous-versions/hh450903(v=vs.85))">简单外围总线</a> (SPB 上，<a href="/windows-hardware/drivers/wdf/overview-of-the-umdf" data-raw-source="[User-Mode Driver Framework](../wdf/overview-of-the-umdf.md)">用户模式驱动程序框架</a>如何 (UMDF) 驱动程序，) 会获得操作设备所需的硬件资源。 这些资源包含驱动程序用于建立到设备的逻辑连接的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/spb/full-duplex-i-o-requests" data-raw-source="[Full-Duplex I/O Requests](./full-duplex-i-o-requests.md)">全双工 I/O 请求</a></p></td>
<td><p>某些总线，如 SPI，支持全双工总线传输。 这些传输通过将数据同时写入设备并从同一设备读取数据来提高 i/o 性能。 为了支持全双工总线传输， <a href="/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](/previous-versions/hh450903(v=vs.85))">简单的外围总线</a> (SPB) <a href="/previous-versions/hh698224(v=vs.85)" data-raw-source="[I/O request interface](/previous-versions/hh698224(v=vs.85))">i/o 请求接口</a> 定义 <a href="https://msdn.microsoft.com/library/windows/hardware/hh974774" data-raw-source="[&lt;strong&gt;IOCTL_SPB_FULL_DUPLEX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh974774)"><strong>IOCTL_SPB_FULL_DUPLEX</strong></a> 的 i/o 控制代码 (IOCTL) 。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/spb/atomic-bus-operations" data-raw-source="[Atomic Bus Operations](./atomic-bus-operations.md)">原子总线操作</a></p></td>
<td><p>若要使用已连接到 SPB 的外围设备的某些硬件功能，SPB 控制器的客户端 (即，外设驱动程序) 可能需要执行与设备之间的数据传输序列作为原子总线操作。 传输序列是原子的，因为任何其他客户端都不能在总线上的设备之间传输数据，直到序列结束。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/spb/spb-connection-locks" data-raw-source="[SPB Connection Locks](./spb-connection-locks.md)">SPB 连接锁</a></p></td>
<td><p>连接锁可用于使两个客户端在 <a href="/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](/previous-versions/hh450903(v=vs.85))">简单外围总线</a> (SPB) 上共享对目标外围设备的访问。 这两个客户端都可以打开到同一目标设备的逻辑连接，并在客户端要求对设备进行独占访问时使用连接锁定，以执行一系列 i/o 操作。 当一台客户端持有连接锁时，第二个客户端对该设备的请求会自动延迟，直到第一个客户端释放该锁。</p></td>
</tr>
</tbody>
</table>

