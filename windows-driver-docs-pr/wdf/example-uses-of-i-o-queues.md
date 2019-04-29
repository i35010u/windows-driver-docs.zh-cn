---
title: I/O 队列的示例使用
description: I/O 队列的示例使用
ms.assetid: 13b09254-ce0a-4c7d-bdb1-d28ec094a266
keywords:
- I/O 队列 WDK KMDF，示例
- 请求处理程序 WDK KMDF
- 默认 I/O 队列 WDK KMDF
- 单个 I/O 队列 WDK KMDF
- 多个 I/O 队列 WDK KMDF
- 并行 I/O 队列 WDK KMDF
- 顺序 I/O 队列 WDK KMDF
- 手动 I/O 队列 WDK KMDF
- I/O 队列 WDK KMDF，调度方法
- 调度方法 WDK KMDF
- 顺序调度 WDK KMDF
- 同步调度 WDK KMDF
- 并行调度 WDK KMDF
- 异步调度 WDK KMDF
- 手动调度 WDK KMDF
- WdfIoQueueDispatchParallel
- WdfIoQueueDispatchSequential
- WdfIoQueueDispatchManual
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3539c02c7fd9a2f20d43049ba8f9a7f5a5238b2f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391358"
---
# <a name="example-uses-of-io-queues"></a>I/O 队列的示例使用





对于连接到的系统和特定的驱动程序支持的每个设备，该驱动程序可以使用以下组合的 I/O 队列和[请求处理程序](request-handlers.md):

-   单个，默认 I/O 队列和单个请求处理程序， [ *EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)。 该框架会将所有设备的请求传送到默认的队列，并且它将调用的驱动程序*EvtIoDefault*处理程序以将每个请求传递到驱动程序。

-   单个，默认 I/O 队列和多个请求处理程序，如[ *EvtIoRead*](https://msdn.microsoft.com/library/windows/hardware/ff541776)， [ *EvtIoWrite*](https://msdn.microsoft.com/library/windows/hardware/ff541813)，和[ *EvtIoDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541758)。 该框架会将所有设备的请求传送到默认的队列中。 它将调用的驱动程序*EvtIoRead*处理程序将读取的请求*EvtIoWrite*传送写入请求的处理程序并*EvtIoDeviceControl*到处理程序提供设备 I/O 控制请求。

-   多个 I/O 队列，例如一个用于读取请求，另一个用于写入请求。 对于每个队列，该驱动程序提供只有一个请求处理程序，因为在队列接收到只有一种类型的请求。

-   多个 I/O 队列，每个都有多个请求处理程序。

一些示例方案包括：

-   [单个的顺序 I/O 队列](#a-single-sequential-io-queue)

-   [多个有序 I/O 队列和手动队列](#multiple-sequential-io-queues-and-a-manual-queue)

-   [单个并行 I/O 队列](#a-single-parallel-io-queue)

-   [多个并行 I/O 队列](#multiple-parallel-io-queues)

## <a name="a-single-sequential-io-queue"></a>单个的顺序 I/O 队列

如果你正在编写功能驱动程序的磁盘驱动器，可以仅服务读取和写入一次一个请求，功能驱动程序需要每个设备只有一个 I/O 队列。

该驱动程序可以使用默认的 I/O 队列由框架创建时驱动程序调用[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)并设置**DefaultQueue**到**TRUE**中的队列[ **WDF\_IO\_队列\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552359)结构。 在 WDF\_IO\_队列\_配置结构，还应指定驱动程序：

-   **WdfIoQueueDispatchSequential**作为调度方法，因此默认 I/O 队列会将传送 I/O 请求到驱动程序以同步方式。

-   单个事件回调函数， [ *EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)，将接收所有 I/O 请求。

每次 I/O 请求时可用的驱动程序的默认 I/O 队列中，框架将传送该请求向驱动程序通过调用在驱动程序[ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)请求处理程序。 如果另一个请求在队列中可用时，框架将不会传递它直到驱动程序调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)先前已传送的请求。

## <a name="multiple-sequential-io-queues-and-a-manual-queue"></a>多个有序 I/O 队列和手动队列

请考虑具有以下特征的串行端口设备：

-   它可以同时执行一个读取操作，一个写入操作。

-   它不能执行多个读取或写入操作以异步方式。

-   它可接收设备 I/O 控制请求的状态信息。 设备的驱动程序可能需要很长时间才能完成某些这些请求 （例如要等待的状态更改请求）。

功能驱动程序为此设备无法使用多个，每台设备进行排队顺序 I/O。 该驱动程序将调用[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)三次： 一次创建的默认队列，另两次以创建两个额外的 I/O 队列。 在中[ **WDF\_IO\_队列\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)结构为每个这些队列，该驱动程序应指定：

-   **WdfIoQueueDispatchSequential**作为每个队列的调度方法，以便该框架将提供给驱动程序的 I/O 请求同步。

-   不同[请求处理程序](request-handlers.md)为每个队列 ([*EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)， [ *EvtIoRead*](https://msdn.microsoft.com/library/windows/hardware/ff541776)，和[*EvtIoWrite*](https://msdn.microsoft.com/library/windows/hardware/ff541813))，其将接收队列的 I/O 请求。

在调用[ **WdfIoQueueCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547401)，该驱动程序可以调用[ **WdfDeviceConfigureRequestDispatching** ](https://msdn.microsoft.com/library/windows/hardware/ff545920)两次-到正向所有读取到一个额外的队列的请求和所有其他写入请求。

使用此配置，设备的默认 I/O 队列[ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)回调函数将接收仅设备 I/O 控制请求的状态信息。

如果该驱动程序必须保存很长时间的状态请求，它可以创建第四个队列，并指定**WdfIoQueueDispatchManual**作为调度方法。 当驱动程序收到的请求必须等待的信息时，它可以请求放入此额外队列之前的状态信息变得可用。 然后，驱动程序可以从队列中检索该请求，并完成它。 在此期间，默认的队列可以将另一个请求传递到驱动程序。

## <a name="a-single-parallel-io-queue"></a>单个并行 I/O 队列

某些 I/O 操作，而不是其他可以重叠 IDE 磁盘控制器。 例如，在一个控制器处理一个磁盘上的读取或写入操作时，它可以发送查找命令到另一个磁盘。 但是，多个同时进行读取和写入命令不支持。

此控制器功能驱动程序必须检查每个 I/O 请求。 如果该驱动程序收到查找命令，它必须确定是否可以处理的查找命令。 如果无法处理的查找命令：

-   指定的磁盘驱动器已正忙。

-   正在格式化磁盘驱动器，因此，任何其他驱动器可以处于活动状态。

对于每个设备连接到控制器，该驱动程序可以调用[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)创建默认 I/O 队列。 在中[ **WDF\_IO\_队列\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)结构为每个这些队列，该驱动程序应指定：

-   **WdfIoQueueDispatchParallel**作为每个队列的调度方法，以便该框架将提供给驱动程序的 I/O 请求以异步方式。

-   [ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)对于每个队列，将接收队列的 I/O 请求的事件的回调函数。

使用此配置，单一、 并行的 I/O 队列分配给每个设备。 该驱动程序必须检查框架提供的每个 I/O 队列从每个 I/O 请求。 如果该驱动程序可以立即处理请求，它会这样。 否则，该驱动程序会调用[ **WdfIoQueueStop**](https://msdn.microsoft.com/library/windows/hardware/ff548482)，这将导致停止之前驱动程序调用提供请求的 framework [ **WdfIoQueueStart**](https://msdn.microsoft.com/library/windows/hardware/ff548478).

## <a name="multiple-parallel-io-queues"></a>多个并行 I/O 队列

SCSI 主机适配器是设备的支持异步、 重叠 I/O 操作的示例。 多达 32 设备可以连接到适配器。 请考虑使用以下配置的系统：

-   某些设备连接到 SCSI 适配器支持"此"，而有些则不。 如果 SCSI 设备支持此，然后在 I/O 操作过程中设备可以暂时释放适配器使适配器可以为服务另一台设备。 第一台设备更高版本会重新选择本身来完成其操作。

-   SCSI 适配器使用硬件邮箱驱动程序和设备之间传递请求和响应。 如果设备已准备就绪的请求，但没有可用的邮箱中，必须等待设备。

为了获得最佳性能，此 SCSI 主机适配器功能驱动程序应该会收到输入/输出请求 framework 立即可用。 驱动程序必须检查每个请求，并确定可以立即启动还是必须推迟到该设备并提供了资源 （如邮箱内存）。

该驱动程序可能应使用多个，并行 I/O 队列。 对于每个设备连接到该适配器，该驱动程序将调用[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)创建默认 I/O 队列。 在中[ **WDF\_IO\_队列\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)结构为每个这些队列，该驱动程序应指定：

-   **WdfIoQueueDispatchParallel**作为每个队列的调度方法，以便该框架将提供给驱动程序的 I/O 请求以异步方式。

-   [ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)对于每个队列，将接收队列的 I/O 请求的事件的回调函数。

每个 I/O 队列[ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)回调函数必须传递的并确定是否每个可以在提供立即检查队列的 I/O 请求。 如果设备和系统资源可用，该驱动程序将启动 I/O 操作。 如果设备或资源不可用，驱动程序必须调用[ **WdfIoQueueStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548482)停止之前可以处理当前传递的其他请求。

（可选） 该驱动程序可以调用[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)若要创建的每个设备的更多队列。 然后，驱动程序可以调用[ **WdfRequestForwardToIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff549958)以对某些类型的附加队列对请求进行重新排队。 当框架提供从其他队列的请求时，该驱动程序可以调用[ **WdfIoQueueStop**](https://msdn.microsoft.com/library/windows/hardware/ff548482)，如果有必要，在该队列而不是默认的队列，因此可尽量减少的数量或类型为其推迟交付的请求。

 

 





