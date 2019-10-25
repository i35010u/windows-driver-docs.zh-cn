---
title: SCSI 端口提供的功能
description: SCSI 端口提供的功能
ms.assetid: 549dc3f1-b62f-4047-bdc0-7e24d5bc6ad5
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 29f34287c19f88b949e2d794fabe5c3ce8d93a03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844508"
---
# <a name="capabilities-provided-by-scsi-port"></a>SCSI 端口提供的功能

SCSI 端口驱动程序提供以下功能：

- Microsoft Windows 支持包含不同类型的 i/o 总线和/或多个相同类型的 i/o 总线的系统。 需要使用常见的寻址方案来处理这种情况。

- PCI 设备可以有 i/o 端口和内存注册资源。 逻辑地址有助于使此区分对端口驱动程序透明。

- 某些系统包含连接到多个总线的 Hba;此类 HBA 可能需要几组地址转换。

- 逻辑地址是对基于 CISC 的计算机和基于 RISC 的计算机之间的可移植性所需的。

- 正在重试 Irp，因为设备太忙而无法处理它们。

    当设备太忙而无法处理时，存储类驱动程序不必实现重试 Irp 的算法。 SCSI 端口驱动程序实现此功能。

- 强制执行请求的超时值。

    类驱动程序为请求设置超时值，SCSI 端口负责强制执行。 但是，SCSI 端口驱动程序可以灵活地强制执行类驱动程序的超时值，从而考虑总线的状态。 例如，如果由 SCSI 端口管理的光纤通道链路降低了20秒，则 SCSI 端口可能会在停机期间挂起超时计数器，因此，在此链接返回10秒后，具有10秒时间的请求将不会失败。 SCSI 端口会增加分配给请求的超时值，以响应 i/o 流量的增加，因为使用较大的 i/o 流量，所以设备需要更多的时间来完成请求。

- 处理目标和控制器繁忙错误，以及传输错误条件（换言之，与总线上实际传输数据相关的错误）。 例如：

  - 总线-奇偶校验错误
  - 选择超时

- 为类驱动程序提供主机适配器限制的相关信息。

    类驱动程序负责控制数据传输的大小，以适应主机总线适配器（HBA）的限制。 不过，SCSI 端口为类驱动程序提供了完成此任务所需的信息。 SCSI 端口将此信息 furnishes 适配器描述符（[STORAGE_ADAPTER_DESCRIPTOR](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)）中，以响应[**IOCTL_STORAGE_QUERY_PROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property) IOCTL 请求。 类驱动程序负责根据此描述符中报告的信息将请求分解为适当大小的块。

- 将总线相对地址转换为逻辑地址。

    查询时，适配器会为 i/o 端口、命令寄存器和控制状态寄存器提供与总线相关的地址。 但是，微型端口驱动程序无法使用与总线相关的地址与其主机总线适配器（HBA）进行通信。 SCSI 端口会将总线相对地址转换为逻辑地址，使微型端口驱动程序可以透明方式访问总线地址。 出现此情况的原因有以下几个：

- 在设备启动之前，确保设备及其所有基础设备已通电（处于 D0 设备电源状态）。

    当设备尚未准备好开机时，SCSI 端口会将对该设备的 D0 请求排队，直到设备准备就绪。

- 将来自类驱动程序的异步请求排队，并将它们同步转发到目标设备。

    类驱动程序不必等待请求完成，然后再发送下一个请求。 SCSI 端口假定对这些请求进行排队，以避免对基础硬件的处理能力产生巨大的处理能力。

- 支持内部 i/o 请求队列的内部和外部管理。

    大多数队列管理操作都是由 SCSI 端口本身启动的。 例如，当发生错误时，SCSI 端口会冻结其队列，并向类驱动程序报告错误条件，以便在处理更多请求之前类驱动程序可以响应。 但是，SCSI 端口还会响应来自类驱动程序或其他较高级别的驱动程序的请求，以便锁定、解除锁定、冻结或解冻其内部请求队列。 较高级别的驱动程序可以使用 SRB_FUNCTION_RELEASE_QUEUE 请求强制 SCSI 端口解冻其内部队列。 有关 "冻结"、"锁定" 或 "解除锁定" 队列的含义的说明，请参阅[SCSI 端口驱动程序的队列管理](scsi-port-driver-s-queue-management.md)。

- 将设备报告的错误转换为 SCSI-3 方法数据格式，以供类驱动程序进行处理。

SCSI 端口通过 SCSI 端口库例程向微型端口驱动程序提供服务。 微型端口驱动程序编写器可调用这些例程，而不是将其提供的功能编码为单一单一端口驱动程序。 使用这些例程的一些最重要的服务如下所示：

- SCSI 端口微型端口驱动程序可以将许多与操作系统相关的初始化操作委托给 SCSI 端口的[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)库例程。 这使得 SCSI 端口微型驱动器驱动程序在不同版本的操作系统之间更易于移植。 有关 SCSI 端口微型端口驱动程序的初始化任务的说明，请参阅[Scsi 微型端口驱动程序的 DriverEntry 例程](scsi-miniport-driver-s-driverentry-routine.md)。

- 非 PnP 设备的 SCSI 端口微型端口驱动程序可代替查找适配器并向 PnP 管理器报告其资源的任务。 这是在[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)中完成的。

- SCSI 端口微型端口驱动程序不初始化驱动程序对象中的调度入口点。 当微型端口驱动程序调用[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)时，SCSI 端口驱动程序代表微型端口驱动程序执行此功能。

- SCSI 端口微型端口驱动程序不使用[**HalTranslateBusAddress**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))将与总线相关的地址转换为逻辑地址。 SCSI 端口微型端口驱动程序通过调用[**ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetdevicebase)来实现此目的。

有关 SCSI 端口可用于 SCSI 端口微型端口驱动程序的库例程的摘要，请参阅[Scsi 端口驱动程序支持例程](scsi-port-driver-support-routines.md)。
