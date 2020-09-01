---
title: Storport 提供的功能
description: Storport 提供的功能
ms.assetid: 30b4d2e4-2004-4d71-8c91-f066e52dd256
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: b07e7d11db1826811f5636fd2e819a4a6fa1466c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191324"
---
# <a name="capabilities-provided-by-storport"></a>Storport 提供的功能

Storport 驱动程序提供以下功能：

- **寻址**

  Microsoft Windows 支持包含不同类型的 i/o 总线和/或多个相同类型的 i/o 总线的系统。 需要使用常见的寻址方案来处理这种情况。

  PCI 设备可以有 i/o 端口和内存注册资源。 逻辑地址有助于使此区分对端口驱动程序透明。

  某些系统包含连接到多个总线的 Hba;此类 HBA 可能需要几组地址转换。

  逻辑地址是对基于 CISC 的计算机和基于 RISC 的计算机之间的可移植性所需的。

- **Retrys 和错误处理**

  - 当设备太忙而无法处理时，存储类驱动程序不必实现重试 Irp 的算法。 Storport 驱动程序实现此功能。

  - 类驱动程序为请求设置超时值，而 Storport 负责强制执行。 但 Storport 驱动程序可以灵活地强制执行类驱动程序的超时值，从而考虑到总线的状态。 例如，如果由 Storport 管理的光纤通道链接丢弃20秒，则 Storport 可能会在停机时间挂起超时计数器，因此，如果在该链接恢复之后10秒内的时间超过10秒，请求将不会失败。 Storport 增加了分配给请求的超时值，以响应 i/o 流量的增加，因为使用较大的 i/o 流量，设备需要更多的时间来完成请求。

  - Storport 处理目标和控制器繁忙错误，并处理传输错误条件 (换言之，与总线上的实际传输数据相关的错误) 。 例如：
    - 总线-奇偶校验错误
    - 选择超时

- **配置、排队和电源状态管理**

  - 向类驱动程序提供主机适配器限制的相关信息：类驱动程序负责控制数据传输的大小，以适应主机总线适配器 (Hba) 的限制。 但 Storport 为类驱动程序提供了完成此任务所需的信息。 Storport 将此信息 furnishes 在适配器描述符中 ([STORAGE_ADAPTER_DESCRIPTOR](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)) ，以响应 IOCTL 请求 ([**IOCTL_STORAGE_QUERY_PROPERTY**](/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)) 。 类驱动程序负责根据此描述符中报告的信息将请求分解为适当大小的块。

  - 将总线相对地址转换为逻辑地址：查询时，适配器会为 i/o 端口、命令寄存器和控制状态寄存器提供与总线相关的地址。 但是，微型端口驱动程序无法使用与总线相关的地址与其主机总线适配器 (HBA) 通信。 Storport 将与总线相关的地址转换为逻辑地址，使微型端口驱动程序可以透明方式访问总线地址。 原因包括：

  - 确保设备及其所有底层设备在设备开始之前处于 D0 设备电源状态) 上 (：当设备尚未准备好开机时，Storport 会将该设备的 D0 请求排队，直到设备准备就绪。

  - 对来自类驱动程序的异步请求进行排队并将它们异步转发到目标设备：类驱动程序不必等待请求完成，然后再发送下一个请求。 Storport 假设需要对这些请求进行排队，以避免对基础硬件的处理能力产生巨大的处理能力。

  - 支持内部 i/o 请求队列的内部和外部管理：最多队列管理操作由 Storport 本身启动。 例如，Storport 在发生错误时冻结其队列，并向类驱动程序报告错误条件，以便在处理更多请求之前类驱动程序可以响应。 但 Storport 还响应类驱动程序或其他较高级别的驱动程序发出的请求，以锁定、解锁、冻结或解冻其内部请求队列。 较高级别的驱动程序可以使用 SRB_FUNCTION_RELEASE_QUEUE 请求强制 Storport 取消冻结其内部队列。 有关 "冻结"、"锁定" 或 "解除锁定" 队列的含义的说明，请参阅 [Storport 队列管理](storport-queue-management.md)。

  - 将设备报告的错误转换为 SCSI-3 感知数据格式，以供类驱动程序进行处理。

Storport 通过 Storport 库例程向微型端口驱动程序提供服务。 微型端口驱动程序编写器可调用这些例程，而不是将其提供的功能编码为单一单一端口驱动程序。 使用这些例程的一些最重要的服务如下所示：

- Storport 微型端口驱动程序可以将许多与操作系统相关的初始化操作委托给 Storport 的 [**StorPortInitialize**](/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize) 库例程。 例如，Storport 驱动程序处理与 PnP 和 DMA 映射相关的详细信息。 这使得在不同版本的操作系统之间更易于移植的 Storport 微型端口驱动程序。 有关 Storport 微型端口驱动程序的初始化任务的说明，请参阅 [使用 storport 进行硬件初始化](hardware-initialization-with-storport.md)。

- 适用于非 PnP 设备的 Storport 微型端口驱动程序可代替查找适配器并向 PnP 管理器报告其资源的任务。 这是在 [**StorPortInitialize**](/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)中完成的。

- Storport 微型端口驱动程序不初始化驱动程序对象中的调度入口点。 当微型端口驱动程序调用 [**StorPortInitialize**](/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)时，Storport 驱动程序会代表微型端口驱动程序执行此功能。

- Storport 微型端口驱动程序不使用 **HalTranslateBusAddress**将与总线相关的地址转换为逻辑地址。 Storport 微型端口驱动程序通过调用 [**StorPortGetDeviceBase**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase)来实现此目的。

有关 Storport 可用于 Storport 微型端口驱动程序的库例程的完整列表，请参阅 [Storport 驱动程序支持例程](storport-driver-support-routines.md)。