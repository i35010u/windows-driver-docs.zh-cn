---
title: SCSI 端口提供的功能
description: SCSI 端口提供的功能
ms.assetid: 549dc3f1-b62f-4047-bdc0-7e24d5bc6ad5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e5f7714f7c41045a4fcf165b0a1d64f7465fc3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368361"
---
# <a name="capabilities-provided-by-scsi-port"></a>SCSI 端口提供的功能


## <span id="ddk_capabilities_provided_by_scsi_port_kg"></span><span id="DDK_CAPABILITIES_PROVIDED_BY_SCSI_PORT_KG"></span>


SCSI 端口驱动程序提供了以下功能：

-   Microsoft Windows 支持包含不同类型的 I/O 总线和/或相同类型的多个 I/O 总线的系统。 常见的寻址方案需要处理这样的多样性。

-   PCI 设备可以有 I/O 端口和注册的资源的内存。 逻辑地址有助于使这一区别对端口驱动程序透明。

-   某些系统包含连接到多个总线; 的 Hba此类 HBA 可能需要多个地址转换的集。

-   逻辑地址需要跨 CISC 基于和 RISC 基于计算机的可移植性。

<!-- -->

-   正在重试 Irp，当设备太忙而无法处理它们。

    存储类驱动程序不需要实现当设备太忙而无法处理它们时重试 Irp 的算法。 SCSI 端口驱动程序实现此功能。

-   强制执行请求的超时值。

    在类驱动程序设置的请求的超时值和 SCSI 端口负责强制执行它。 但是，SCSI 端口驱动程序可以强制执行的类驱动程序的超时值功能，灵活地，采用纳入考虑范围的总线的状态。 例如，如果由 SCSI 端口管理的光纤通道链接降至 20 秒，SCSI 端口可能期间的挂起超时计数器停机时间，以便例如，10 秒的超时请求之前，将不失败后链接恢复正常后 10 秒。 SCSI 端口会增加分配给请求以增加的 I/O 流量，响应的超时值，因为设备将使用更大的 I/O 流量，需要更多时间来完成请求。

-   处理目标和控制器忙的错误，以及传输错误条件 （即，与实际总线上的数据传输相关的错误）。 例如：

-   1.  总线奇偶校验错误
    2.  所选内容的超时

<!-- -->

-   提供有关主机适配器限制的信息的类驱动程序。

    它负责的类驱动程序来控制数据传输，以满足主机总线适配器 (HBA) 的限制的大小。 但是，SCSI 端口提供的类驱动程序使用它来完成此任务所需的信息。 SCSI 端口提供此适配器描述符中的信息 ([**存储\_适配器\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)) 以响应[ **IOCTL\_存储\_查询\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property) IOCTL 请求。 在类驱动程序负责请求分解为多个块的基于此描述符中报告的信息的适当大小。

-   正在转换到逻辑地址总线相对地址。

    查询时，适配器提供 I/O 端口、 命令寄存器和控件状态寄存器总线相对的地址。 但是，微型端口驱动程序不能使用总线相对地址与其主机总线适配器 (HBA) 进行通信。 SCSI 端口转换到逻辑地址，总线相对地址，以便微型端口驱动程序可以透明方式访问总线地址。 有几个原因：

-   确保，在设备和其基础的所有设备都已打开 （在 D0 设备电源状态） 之前启动设备。

    当设备未准备好打开设备电源时，SCSI 端口队列 D0 请求为该设备之前设备已准备就绪。

-   队列类驱动程序的异步请求并将它们转发到目标设备的同步。

    类驱动程序无需等待发送的下一个请求之前完成的请求。 SCSI 端口有责任队列这些请求以避免庞大的基础硬件的处理能力。

-   支持内部 I/O 请求队列的内部和外部的管理。

    大多数队列管理操作是由 SCSI 端口本身启动的。 例如，SCSI 端口时，会冻结其队列错误发生，向类驱动程序，报告错误条件，以便进一步处理请求之前，可以响应的类驱动程序。 但是，SCSI 端口也响应来自请求的类驱动程序或其他更高级别的驱动程序锁定、 解锁、 冻结或解冻其内部请求队列。 更高级别的驱动程序可以强制 SCSI 端口取消其内部队列使用 SRB\_函数\_发行\_排队请求。 这意味着"冻结"的说明，为"锁定"或"解锁"队列，请参阅[SCSI 端口驱动程序的队列管理](scsi-port-driver-s-queue-management.md)。

-   正在转换报告的错误是由设备为 SCSI 2 检测数据格式，以便处理类驱动程序。

SCSI 端口通过 SCSI 端口库例程提供给微型端口驱动程序的服务。 微型端口驱动程序编写人员可以调用这些例程，而不是无需编码到单个整体式端口驱动程序提供的功能。 一些最重要的服务使用这些例程提供如下所示：

-   SCSI 端口微型端口驱动程序可以很多依赖于 OS 的初始化将操作委托给 SCSI 端口[ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)库例程。 这使 SCSI 端口微型端口驱动程序更易于移植跨不同版本的操作系统。 SCSI 端口微型端口驱动程序初始化任务的说明，请参阅[SCSI 微型端口驱动程序 DriverEntry 例程](scsi-miniport-driver-s-driverentry-routine.md)。

-   SCSI 端口微型端口驱动程序适用于非 PnP 设备空闲下来，查找适配器并向即插即用管理器报告其资源的任务。 这是在[ **ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)。

-   SCSI 端口微型端口驱动程序未初始化的驱动程序对象中的调度入口点。 SCSI 端口驱动程序执行此代表微型端口驱动程序微型端口驱动程序调用时[ **ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)。

-   SCSI 端口微型端口驱动程序不会转换为使用的逻辑地址总线相对地址[ **HalTranslateBusAddress**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))。 SCSI 端口微型端口驱动程序执行此操作通过调用[ **ScsiPortGetDeviceBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportgetdevicebase)。

SCSI 端口使其可供 SCSI 端口微型端口驱动程序的库例程的完整列表，请参阅[SCSI 端口库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

 

 




