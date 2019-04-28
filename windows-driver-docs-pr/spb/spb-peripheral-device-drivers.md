---
title: SPB 外围设备驱动程序
description: 存储外围设备驱动程序控制外围设备连接到简单的外围总线 （存储）。
ms.assetid: 8352EBD9-D94C-4EC6-A17E-3A72DDE4C16C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 898ef8984e290c923d5e166a65cc84dfb0108cca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344998"
---
# <a name="spb-peripheral-device-drivers"></a>SPB 外围设备驱动程序


SPB 外围设备驱动程序控制连接到[简单外设总线](https://msdn.microsoft.com/library/windows/hardware/hh450903) (SPB) 的外围设备。 此设备的硬件寄存器只能通过 SPB 使用。 若要从设备读取数据或向其写入数据，驱动程序必须将 I/O 请求发送到 SPB 控制器。 只有该控制器可以通过 SPB 启动将数据传输到设备或从设备传输数据的过程。

从 Windows 8 开始，Windows 提供的驱动程序支持外围设备的有关[简单的外围总线](https://msdn.microsoft.com/library/windows/hardware/hh450903)(SPBs)。 SPBs，如 I²C 和 SPI，广泛用于连接到较慢的传感器的设备，如加速感应器、 GPS 设备和电池电量水平监视器。 本概述介绍了存储外围设备驱动程序，与其他系统组件，如何控制与存储连接的外围设备。

存储外围设备驱动程序可以生成要使用两种[用户模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff560442)(UMDF) 或[内核模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF)。 有关开发 UMDF 驱动程序的详细信息，请参阅[入门 UMDF](https://msdn.microsoft.com/library/windows/hardware/ff554928)。 有关开发 KMDF 驱动程序的详细信息，请参阅[开始使用内核模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/dn265580)。

## <a name="device-configuration-information"></a>设备配置信息


与存储连接的外围设备的硬件寄存器不是内存映射。 只能通过按顺序将数据传入和传出设备传输上存储的存储控制器可以访问该设备。 若要执行 I/O 操作，存储外围设备驱动程序将 I/O 请求发送到设备，并存储控制器执行完成这些请求所需的数据传输。 有关可以发送到上 SPBs 外围设备的 I/O 请求的详细信息，请参阅[使用存储 I/O 请求接口](https://msdn.microsoft.com/library/windows/hardware/hh698227)。

下图显示的示例硬件配置，在其中存储 — 在这种情况下，I²C 总线 — 两个外围设备连接到芯片 (SoC) 模块上的系统。 外围设备外部的 SoC 模块并连接到的模块上的四个插针。 SoC 模块包含主处理器 （未显示），以及 I²C 控制器和一个[常规用途的 I/O](https://msdn.microsoft.com/library/windows/hardware/hh439512) (GPIO) 控制器。 处理器使用 I²C 控制器来按顺序将数据传入或从两个外围设备。 这些设备中的中断请求行连接到配置为中断输入的两个 GPIO 插针。 当设备向发出信号的中断请求时，GPIO 控制器中继到处理器的中断。

![存储外围设备的连接](images/spbconnects.png)

由于此示例中的 I²C 控制器和 GPIO 控制器集成到 SoC 模块中，其硬件寄存器内存映射和处理器可以直接访问。 但是，处理器可以访问两个外围设备的硬件寄存器仅间接通过 I²C 控制器。

存储不是[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)(PnP) 总线的和，因此，不能使用自动检测并配置新设备插入到总线。 与存储连接的总线和中断连接是设备的经常永久性的。 即使可以从一个槽拔出设备，此槽通常致力于为该设备。 此外，存储不提供来中继到总线控制器的中断请求从外围设备总线上的带内硬件路径。 相反，中断的硬件路径是独立于总线控制器。

供应商的硬件平台将与存储连接的外围设备的配置信息存储在该平台的 ACPI 固件。 在系统启动期间[ACPI 驱动程序枚举](https://msdn.microsoft.com/library/windows/hardware/ff536138)总线上的即插即用的管理器的设备。 为每个枚举设备 ACPI 提供了有关设备的总线和中断连接的信息。 PnP 管理器将此信息存储在名为的数据存储*资源中心*。

即插即用管理器设备启动时，提供设备的驱动程序和一套[硬件资源](https://msdn.microsoft.com/library/windows/hardware/ff547012)，它封装资源中心存储设备的配置信息。 这些资源包括连接 ID，中断数。 连接 ID 封装总线连接信息，如存储控制器、 总线地址和总线时钟频率。 输入/输出请求可以发送到设备之前，驱动程序必须首先使用的连接 ID 以打开到设备的逻辑连接。 中断数是驱动程序可以其中断服务例程 (ISR) 连接到的 Windows 中断资源。 该驱动程序可以轻松地移植从不同的硬件平台到另一个因为连接 ID 和中断号为隐藏的物理总线和中断连接的相关的特定于平台的信息的高级抽象概念。

## <a name="software-and-hardware-layers"></a>软件和硬件层


以下块图显示上存储将外围设备连接到应用程序使用该设备的软件和硬件层。 在此示例中的存储外围设备驱动程序是一个 UMDF 驱动程序。 外围设备 （在关系图的底部） 是传感器设备 （例如，加速感应器）。 上图中，如外围设备连接到 I²C 总线和信号中断请求通过 GPIO 控制器上的 pin。

![连接存储的传感器设备的软件和硬件层](images/spblayers.png)

以灰色显示的三个块都是系统提供的模块。 从 Windows 7 开始[传感器类扩展](https://msdn.microsoft.com/library/windows/hardware/ff545398)可用作 UMDF 的特定于传感器的扩展。 从 Windows 8 开始[存储框架扩展](https://msdn.microsoft.com/library/windows/hardware/hh406203)(SpbCx) 和[GPIO 框架扩展](https://msdn.microsoft.com/library/windows/hardware/hh439512)(GpioClx) 可为 KMDF 执行特定于存储控制器的功能的扩展和到 GPIO 控制器中，分别。

在上面的关系图的顶部，应用程序调用的方法[传感器 API](https://msdn.microsoft.com/library/windows/desktop/dd318953)或[位置 API](https://msdn.microsoft.com/library/windows/desktop/dd464636)与传感器设备进行通信。 通过这些调用，应用程序可以将 I/O 请求发送到设备，并从设备接收事件通知。 有关这些 Api 的详细信息，请参阅[传感器和位置在 Windows 平台简介](https://msdn.microsoft.com/library/windows/hardware/ff545493)。

当应用程序调用时需要与存储外围设备驱动程序的通信的方法时，传感器 API 或位置 API 创建的 I/O 请求并将其发送到存储外围设备驱动程序。 传感器类扩展模块帮助处理这些 I/O 请求驱动程序。 该驱动程序收到新的 I/O 请求时，该驱动程序立即将请求传递到传感器类扩展，从而对请求进行排队，直到该驱动程序已准备好处理它。 如果 I/O 请求从应用程序需要的或从外围设备的数据传输，存储外围设备驱动程序对于此传输创建的 I/O 请求，并将请求发送到 I²C 控制器。 由 SpbCx 和 I²C 控制器驱动程序，共同处理此类请求。

SpbCx 是一个系统提供的组件，用于管理的存储控制器，例如 I²C 控制器在此示例中的 I/O 请求队列。 I²C 控制器驱动程序，由控制器的硬件供应商提供，管理 I²C 控制器中的所有特定于硬件的操作。 例如，控制器驱动程序访问的控制器来启动数据传输到和从外围设备通过 I²C 总线的内存映射硬件寄存器。

外围设备发出信号的中断请求硬件事件发生时需要特别注意存储外围设备驱动程序或用户模式应用程序。 从外围设备的中断行连接到配置为接收中断请求 GPIO 插针。 当设备向发出信号中断到 GPIO 插针时，GPIO 控制器发出信号中断处理器。 在此中断响应，内核的中断的陷阱处理程序调用 GpioClx 的 ISR. 此 ISR 查询 GPIO 控制器驱动程序，然后访问 GPIO 控制器来标识中断的 GPIO 插针的内存映射硬件寄存器。 提示中断、 GPIO 控制器驱动程序 （如果中断是边缘触发） 或者清除或掩码 (如果级别触发) 处 GPIO pin 的中断请求。 必须关闭中断，以防止处理器时的陷阱处理程序返回再次执行相同的中断。 对于级别触发的中断，存储外围设备驱动程序中的 ISR 必须访问要清除中断之前 GPIO pin 可以是未屏蔽的外围设备的硬件寄存器。

内核的中断的陷阱处理程序返回之前，它会安排在存储外围设备驱动程序在 IRQL 运行 ISR = 被动\_级别。 从 Windows 8 开始，UMDF 驱动程序可以连接其 ISR 中断驱动程序收到作为抽象 Windows 中断资源;有关详细信息，请参阅[处理中断](https://msdn.microsoft.com/library/windows/hardware/hh439600)。 若要确定哪些 ISR 调用，操作系统将查找分配到中断的 GPIO 插针和查找连接到中断 ISR 的虚拟中断了。 此虚拟中断标记为*辅助*在上图中的中断。 与此相反，从 GPIO 控制器的硬件中断标记为*主*中断。

在被动级别运行时存储外围设备驱动程序中的 ISR，因为 ISR 可用于同步 I/O 请求访问外围设备中的硬件寄存器。 ISR 可阻止，直到这些请求完成。 ISR，其运行速度相对较高优先级，应尽快返回，并推迟所有后台处理到运行在较低优先级的辅助角色例程中断。

辅助中断响应，存储外围设备驱动程序将事件发送传感器类扩展，这将告知用户模式应用程序通过传感器 API 或位置 API 的事件中。

## <a name="in-this-section"></a>本节内容


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698227" data-raw-source="[Using the SPB I/O Request Interface](https://msdn.microsoft.com/library/windows/hardware/hh698227)">使用存储 I/O 请求接口</a></p></td>
<td><p>从 Windows 8 开始<a href="https://msdn.microsoft.com/library/windows/hardware/hh406203" data-raw-source="[SPB framework extension](https://msdn.microsoft.com/library/windows/hardware/hh406203)">存储框架扩展</a>(SpbCx) 是系统提供的组件，它支持<a href="https://msdn.microsoft.com/library/windows/hardware/hh698224" data-raw-source="[SPB I/O request interface](https://msdn.microsoft.com/library/windows/hardware/hh698224)">存储 I/O 请求接口</a>。 存储外围设备驱动程序使用此接口将 I/O 请求发送到设备连接到 I²C、 SPI，和其他<a href="https://msdn.microsoft.com/library/windows/hardware/hh450903" data-raw-source="[simple peripheral buses](https://msdn.microsoft.com/library/windows/hardware/hh450903)">简单的外围总线</a>(SPBs)。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698216" data-raw-source="[Connection IDs for SPB-Connected Peripheral Devices](https://msdn.microsoft.com/library/windows/hardware/hh698216)">连接存储的外围设备的连接 Id</a></p></td>
<td><p>驱动程序可以外围设备向发送 I/O 请求之前<a href="https://msdn.microsoft.com/library/windows/hardware/hh450903" data-raw-source="[simple peripheral bus](https://msdn.microsoft.com/library/windows/hardware/hh450903)">简单的外围总线</a>（存储），该驱动程序必须打开到设备的逻辑连接。 通过此连接，该驱动程序可以发送读取和写入请求来传输设备数据。 此外，驱动程序可以发送 I/O 控制 (IOCTL) 请求到设备来执行特定于存储的操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698223" data-raw-source="[SPB Device Stacks](https://msdn.microsoft.com/library/windows/hardware/hh698223)">存储设备堆栈</a></p></td>
<td><p>Windows 驱动程序模型完全分离开来控制外围设备 （例如，温度传感器） 的驱动程序组件的总线上管理来回传输数据和控制信息的总线控制器的驱动程序组件外围设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698218" data-raw-source="[Interrupts from SPB-Connected Peripheral Devices](https://msdn.microsoft.com/library/windows/hardware/hh698218)">从存储连接的外围设备的中断</a></p></td>
<td><p>与不同的是如 PCI 总线<a href="https://msdn.microsoft.com/library/windows/hardware/hh450903" data-raw-source="[simple peripheral bus](https://msdn.microsoft.com/library/windows/hardware/hh450903)">简单的外围总线</a>（存储），如 I²C 或 SPI，标准化的不提供特定于总线的意味着要传达给处理器的中断请求从外围设备。 与之相反，通过 SPB 连接的外围设备通过单独的硬件路径来指示某个中断，该路径位于 SPB 和 SPB 控制器外部。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698217" data-raw-source="[Hardware Resources for Kernel-Mode SPB Peripheral Drivers](https://msdn.microsoft.com/library/windows/hardware/hh698217)">内核模式存储外围设备驱动程序的硬件资源</a></p></td>
<td><p>此主题演示中的代码示例如何<a href="https://msdn.microsoft.com/library/windows/hardware/ff544296" data-raw-source="[Kernel-Mode Driver Framework](https://msdn.microsoft.com/library/windows/hardware/ff544296)">内核模式驱动程序框架</a>外围设备上的 (KMDF) 驱动程序<a href="https://msdn.microsoft.com/library/windows/hardware/hh450903" data-raw-source="[simple peripheral bus](https://msdn.microsoft.com/library/windows/hardware/hh450903)">简单的外围总线</a>（存储） 获取到它需要的硬件资源操作设备。 这些资源中包含的是驱动程序使用建立的逻辑连接到设备的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh450837" data-raw-source="[Hardware Resources for User-Mode SPB Peripheral Drivers](https://msdn.microsoft.com/library/windows/hardware/hh450837)">用户模式下存储外围设备驱动程序的硬件资源</a></p></td>
<td><p>此主题演示中的代码示例如何<a href="https://msdn.microsoft.com/library/windows/hardware/ff560442" data-raw-source="[User-Mode Driver Framework](https://msdn.microsoft.com/library/windows/hardware/ff560442)">用户模式驱动程序框架</a>外围设备上的 (UMDF) 驱动程序<a href="https://msdn.microsoft.com/library/windows/hardware/hh450903" data-raw-source="[simple peripheral bus](https://msdn.microsoft.com/library/windows/hardware/hh450903)">简单的外围总线</a>（存储） 获取其运行所需的硬件资源设备。 这些资源中包含的是驱动程序使用建立的逻辑连接到设备的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh974772" data-raw-source="[Full-Duplex I/O Requests](https://msdn.microsoft.com/library/windows/hardware/hh974772)">全双工 I/O 请求</a></p></td>
<td><p>某些总线，例如 SPI，支持完全双工总线传输。 这些传输提高 I/O 性能数据写入到设备，同时在同一设备读取数据。 若要支持全双工总线传输<a href="https://msdn.microsoft.com/library/windows/hardware/hh450903" data-raw-source="[simple peripheral bus](https://msdn.microsoft.com/library/windows/hardware/hh450903)">简单的外围总线</a>（存储） <a href="https://msdn.microsoft.com/library/windows/hardware/hh698224" data-raw-source="[I/O request interface](https://msdn.microsoft.com/library/windows/hardware/hh698224)">I/O 请求接口</a>定义<a href="https://msdn.microsoft.com/library/windows/hardware/hh974774" data-raw-source="[&lt;strong&gt;IOCTL_SPB_FULL_DUPLEX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh974774)"> <strong>IOCTL_SPB_FULL_DUPLEX</strong> </a>I/O 控制代码 (IOCTL)。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/jj850339" data-raw-source="[Atomic Bus Operations](https://msdn.microsoft.com/library/windows/hardware/jj850339)">原子总线操作</a></p></td>
<td><p>若要使用的与存储连接的外围设备的某些硬件功能，存储控制器 （即外围设备驱动程序） 的客户端可能需要执行一系列数据传输到和从设备作为一个原子总线操作。 因为在总线上没有其他客户端传输到或从设备的数据序列完成之前，传输序列是原子的。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/jj819326" data-raw-source="[SPB Connection Locks](https://msdn.microsoft.com/library/windows/hardware/jj819326)">存储连接锁</a></p></td>
<td><p>连接锁可用于启用两个客户端上共享到目标外围设备的访问权限<a href="https://msdn.microsoft.com/library/windows/hardware/hh450903" data-raw-source="[simple peripheral bus](https://msdn.microsoft.com/library/windows/hardware/hh450903)">简单的外围总线</a>（存储）。 两个客户端可以打开到相同的目标设备的逻辑连接，并使用连接锁时客户端要求对设备执行一系列 I/O 操作的独占访问。 当一台客户端持有连接锁时，第二个客户端请求来访问设备是自动推迟到第一个客户端释放锁。</p></td>
</tr>
</tbody>
</table>

 

 

 




