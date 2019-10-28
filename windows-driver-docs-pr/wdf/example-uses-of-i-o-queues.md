---
title: I/o 队列的示例用法
description: I/o 队列的示例用法
ms.assetid: 13b09254-ce0a-4c7d-bdb1-d28ec094a266
keywords:
- I/o 队列 WDK KMDF，示例
- 请求处理程序 WDK KMDF
- 默认 i/o 队列 WDK KMDF
- 单 i/o 队列 WDK KMDF
- 多个 i/o 队列 WDK KMDF
- 并行 i/o 队列 WDK KMDF
- 顺序 i/o 队列 WDK KMDF
- 手动 i/o 队列 WDK KMDF
- I/o 队列 WDK KMDF，调度方法
- 调度方法 WDK KMDF
- 顺序分派 WDK KMDF
- 同步分派 WDK KMDF
- 并行分派 WDK KMDF
- 异步分派 WDK KMDF
- 手动分派 WDK KMDF
- WdfIoQueueDispatchParallel
- WdfIoQueueDispatchSequential
- WdfIoQueueDispatchManual
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34c9f4be46d24a8baf6cf218f526ad7cc23e8b7b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843188"
---
# <a name="example-uses-of-io-queues"></a>I/o 队列的示例用法





对于连接到系统并受特定驱动程序支持的每个设备，驱动程序可以使用 i/o 队列和[请求处理程序](request-handlers.md)的下列组合：

-   单个、默认 i/o 队列和单个请求处理程序[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)。 该框架将向默认队列提供设备的所有请求，并调用驱动程序的*EvtIoDefault*处理程序，将每个请求传递给驱动程序。

-   单个默认 i/o 队列和多个请求处理程序，如[*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)、 [*EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)和[*EvtIoDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)。 该框架会将设备的所有请求传递到默认队列。 它将调用驱动程序的*EvtIoRead*处理程序来传递读取请求、传递写入请求的*EvtIoWrite*处理程序，以及用于传递设备 I/o 控制请求的*EvtIoDeviceControl*处理程序。

-   多个 i/o 队列，例如一个用于读取请求，另一个用于写入请求。 对于每个队列，驱动程序只提供一个请求处理程序，因为队列只接收一种类型的请求。

-   多个 i/o 队列，每个队列都有多个请求处理程序。

某些示例方案包括：

-   [单顺序 i/o 队列](#a-single-sequential-io-queue)

-   [多个顺序 i/o 队列和手动队列](#multiple-sequential-io-queues-and-a-manual-queue)

-   [单个并行 i/o 队列](#a-single-parallel-io-queue)

-   [多个并行 i/o 队列](#multiple-parallel-io-queues)

## <a name="a-single-sequential-io-queue"></a>单顺序 i/o 队列

如果要为每次只提供一次读取和写入请求的磁盘驱动器编写函数驱动程序，则函数驱动程序每个设备只需要一个 i/o 队列。

驱动程序可以使用在驱动程序调用[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)时框架创建的默认 i/o 队列，并在队列的[**WDF\_IO\_队列\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)结构中将**DefaultQueue**设置为**TRUE** 。 在 WDF\_IO\_QUEUE\_CONFIG 结构中，驱动程序还应指定：

-   **WdfIoQueueDispatchSequential**作为调度方法，因此默认 i/o 队列将同步向驱动程序提供 i/o 请求。

-   单个事件回调函数[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)，它将接收所有 i/o 请求。

每次 i/o 请求在驱动程序的默认 i/o 队列中可用时，框架会通过调用驱动程序的[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)请求处理程序将请求传递给驱动程序。 如果队列中有另一个请求可用，则该框架将不会传递该请求，直到驱动程序为之前传递的请求调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 。

## <a name="multiple-sequential-io-queues-and-a-manual-queue"></a>多个顺序 i/o 队列和手动队列

假设串行端口设备具有以下特征：

-   它可以同时执行一个读取操作和一个写入操作。

-   它无法以异步方式执行多个读取或写入操作。

-   它可以接收设备 i/o 控制请求以获取状态信息。 设备的驱动程序可能需要很长时间才能完成其中一些请求（例如等待状态更改的请求）。

此设备的函数驱动程序可以对每个设备使用多个顺序 i/o 队列。 驱动程序将调用[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)三次：一次是创建默认队列，另外两次创建两个额外的 i/o 队列。 在[**WDF\_IO\_队列\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)每个队列的配置结构中，驱动程序应指定：

-   **WdfIoQueueDispatchSequential**作为每个队列的调度方法，以便框架能够同步地向驱动程序提供 i/o 请求。

-   每个队列的不同[请求处理程序](request-handlers.md)（[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)、 [*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)和[*EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)）将接收队列的 i/o 请求。

在调用[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)之后，驱动程序可以调用[**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)两次，以便将所有读取请求转发到其中一个额外队列和所有写入请求。

通过此配置，设备的默认 i/o queue [*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)回调函数将只接收设备 i/o 控制请求的状态信息。

如果驱动程序必须长时间保存状态请求，则可以创建第四个队列，并将**WdfIoQueueDispatchManual**指定为调度方法。 当驱动程序收到它必须等待的信息的请求时，它可以将请求放入此额外的队列，直到状态信息变为可用。 然后，该驱动程序可以从队列中检索该请求并完成它。 同时，默认队列可以向驱动程序提供另一个请求。

## <a name="a-single-parallel-io-queue"></a>单个并行 i/o 队列

IDE 磁盘控制器可能会重叠某些 i/o 操作，而不是其他操作。 例如，当控制器正在处理一个磁盘上的读取或写入操作时，它可以向另一个磁盘发送搜寻命令。 另一方面，不支持多个并发读取和写入命令。

此控制器的函数驱动程序必须检查每个 i/o 请求。 如果驱动程序收到查找命令，则必须确定是否可以处理 seek 命令。 如果是以下情况，则无法处理 seek 命令：

-   指定的磁盘驱动器已忙。

-   磁盘驱动器正在格式化，因此没有其他驱动器处于活动状态。

对于每个连接到控制器的设备，驱动程序可以调用[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)来创建默认 i/o 队列。 在[**WDF\_IO\_队列\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)每个队列的配置结构中，驱动程序应指定：

-   **WdfIoQueueDispatchParallel**作为每个队列的调度方法，以使框架能够以异步方式将 i/o 请求传递给驱动程序。

-   每个队列的[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)事件回叫函数，将接收队列的 i/o 请求。

使用此配置时，将为每个设备分配一个并行 i/o 队列。 驱动程序必须检查框架从每个 i/o 队列提供的每个 i/o 请求。 如果驱动程序可以立即处理请求，则会执行此操作。 否则，驱动程序将调用[**WdfIoQueueStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)，这会导致框架停止传递请求，直到驱动程序调用[**WdfIoQueueStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestart)。

## <a name="multiple-parallel-io-queues"></a>多个并行 i/o 队列

SCSI 主机适配器是支持异步、重叠 i/o 操作的设备示例。 最多可将32台设备连接到适配器。 假设系统具有以下配置：

-   某些连接到 SCSI 适配器的设备支持 "reselection"，某些设备不支持 ""。 如果 SCSI 设备支持 reselection，则在 i/o 操作过程中，设备可能会暂时释放适配器，以便适配器可以为其他设备服务。 第一个设备稍后 reselects 其操作完成。

-   SCSI 适配器使用硬件邮箱来传递驱动程序和设备之间的请求和响应。 如果设备已准备好进行请求，但没有可用的邮箱，则设备必须等待。

为了获得最佳性能，此 SCSI 主机适配器的函数驱动程序应在其可用时立即从框架接收 i/o 请求。 该驱动程序必须检查每个请求，并确定它是否可以立即启动，或者在设备和资源（如邮箱内存）可用之前必须将其推迟。

驱动程序可能会使用多个并行 i/o 队列。 对于连接到适配器的每个设备，驱动程序将调用[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)来创建默认 i/o 队列。 在[**WDF\_IO\_队列\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)每个队列的配置结构中，驱动程序应指定：

-   **WdfIoQueueDispatchParallel**作为每个队列的调度方法，以使框架能够以异步方式将 i/o 请求传递给驱动程序。

-   每个队列的[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)事件回叫函数，将接收队列的 i/o 请求。

每个 i/o 队列的[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)回调函数都必须在传递队列时检查队列的 i/o 请求，并确定是否可以立即处理每个请求。 如果设备和系统资源可用，则驱动程序将启动 i/o 操作。 如果该设备或资源不可用，则驱动程序必须调用[**WdfIoQueueStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)来停止发送其他请求，直到可以处理当前的请求。

或者，驱动程序可以调用[**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)为每个设备创建其他队列。 然后，驱动程序可以调用[**WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue) ，将某些类型的请求重新排队到其他队列。 当框架从其他队列传递请求时，驱动程序可以在该队列（而不是默认队列）上调用[**WdfIoQueueStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop)，从而最大程度地减少延迟传递的请求的数量或类型。

 

 





