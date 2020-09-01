---
title: I/O 请求的调度方法
description: I/O 请求的调度方法
ms.assetid: 3e91aa7c-bccf-4eeb-8b68-b1277a690f8c
keywords:
- I/o 队列 WDK KMDF，创建
- I/o 队列 WDK KMDF，调度方法
- 调度方法 WDK KMDF
- 顺序分派 WDK KMDF
- 同步分派 WDK KMDF
- 并行分派 WDK KMDF
- 异步分派 WDK KMDF
- 手动分派 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7dbfeaa435c769185cd6fcfbc5786a945b0483f6
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188729"
---
# <a name="dispatching-methods-for-io-requests"></a>I/O 请求的调度方法





当驱动程序调用 [**WdfIoQueueCreate**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate) 来创建 i/o 队列时，它将为队列指定调度方法。 该框架提供了三种调度方法： [顺序](#sequential-dispatching)、 [并行](#parallel-dispatching)和 [手动](#manual-dispatching)。 驱动程序可以为任何 i/o 队列指定任意一种调度方法，包括设备的 [默认 i/o 队列](creating-i-o-queues.md)。

驱动程序通过在队列的[**wdf \_ io \_ 队列 \_ CONFIG**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)结构中指定[**WDF \_ io \_ 队列 \_ 调度 \_ 类型**](/windows-hardware/drivers/ddi/wdfio/ne-wdfio-_wdf_io_queue_dispatch_type)的值来设置队列的调度方法。

有关使用每个调度方法的示例，请参阅 [I/o 队列的使用示例](example-uses-of-i-o-queues.md)。

### <a name="sequential-dispatching"></a><a href="" id="sequential-dispatching"></a> 顺序调度

如果你的驱动程序或设备一次只能处理一个队列的 i/o 请求，则应将设备的 i/o 队列设置为使用 *顺序调度*，这也称为 *同步分派*。 对于这种类型的调度，框架每次将请求传递给驱动程序。 在驱动程序 [完成](completing-i-o-requests.md)、 [取消](canceling-i-o-requests.md)或 [会](requeuing-i-o-requests.md) 上一个请求之前，框架不会传递下一个请求。

在框架将请求传递给某个驱动程序的 [请求处理](request-handlers.md)程序后，该驱动程序将 [处理该请求](processing-i-o-requests.md)。 如果驱动程序将请求转发到 [一般 i/o 目标](general-i-o-targets.md)，则通常会调用 i/o 目标对象的同步方法之一。 有关这些方法的详细信息，请参阅 [同步发送 I/o 请求](sending-i-o-requests-synchronously.md)。 驱动程序最终必须 [完成](completing-i-o-requests.md) 或 [取消](canceling-i-o-requests.md) 从 i/o 队列接收的每个请求。

为顺序调度设置 i/o 队列的驱动程序可以调用 [**WdfIoQueueRetrieveNextRequest**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest) 或 [**WdfIoQueueRetrieveRequestByFileObject**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject) ，以在最后接收的请求完成或取消之前从队列中获取另一个请求。 你可能想要在函数驱动程序中执行此操作，以便驱动程序可以启动下一个硬件操作，同时驱动程序的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 回调函数仍在处理以前的硬件操作的数据。

如果创建多个 i/o 队列并将它们全部设置为顺序调度，则该框架将按顺序调度每个队列的请求，但队列将并行运行。 如果你的驱动程序或设备一次只能处理一个请求，则必须使用具有 [*EvtIoDefault*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default) 回调函数的单个 i/o 队列。

### <a name="parallel-dispatching"></a><a href="" id="parallel-dispatching"></a> 并行调度

如果驱动程序和设备可以同时处理多个 i/o 请求，则可以设置设备的 i/o 队列以使用 *并行调度* ，以便驱动程序可以异步处理请求。 此调度方法也称为 *异步分派*。

如果驱动程序将 i/o 队列设置为使用并行调度，则当队列中有可用的驱动程序时，框架会立即将 i/o 请求发送到该驱动程序。 因此，驱动程序可能必须一次处理多个请求。

每次驱动程序的 [请求处理程序](request-handlers.md) 之一收到请求时，驱动程序必须 [处理该请求](processing-i-o-requests.md) ，然后 [完成](completing-i-o-requests.md) 该请求。 如果驱动程序将请求转发到 [一般 i/o 目标](general-i-o-targets.md)，则通常会调用某个 i/o 目标对象的异步方法。 有关这些方法的详细信息，请参阅 [异步发送 I/o 请求](sending-i-o-requests-asynchronously.md)。 驱动程序最终必须 [完成](completing-i-o-requests.md) 或 [取消](canceling-i-o-requests.md) 从 i/o 队列接收的每个请求。

使用并行调度的驱动程序可以调用 [**WdfIoQueueStop**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestop) 或 [**WdfIoQueueStopSynchronously**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestopsynchronously) 来暂时停止队列，然后调用 [**WdfIoQueueStart**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuestart) 来重新启动队列。

### <a name="manual-dispatching"></a><a href="" id="manual-dispatching"></a> 手动分派

如果希望驱动程序能够完全控制 i/o 请求的传送，则可以设置设备的 i/o 队列以使用 *手动调度*，这意味着框架不会将请求传递给驱动程序，除非驱动程序显式请求一个。

若要获取手动队列的请求，驱动程序可以在轮询队列的循环中调用 [**WdfIoQueueRetrieveNextRequest**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrievenextrequest) 或 [**WdfIoQueueRetrieveRequestByFileObject**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject) 。 或者，驱动程序可以调用 [**WdfIoQueueReadyNotify**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuereadynotify) 来注册一个回调函数，当队列中有一个或多个请求可用时，框架将调用该函数。 在框架调用回调函数后，驱动程序可以在循环中调用 **WdfIoQueueRetrieveNextRequest** 或 **WdfIoQueueRetrieveRequestByFileObject** 来检索请求。

驱动程序从队列中获取请求后，必须 [处理该请求](processing-i-o-requests.md)。 驱动程序最终必须 [完成](completing-i-o-requests.md) 或 [取消](canceling-i-o-requests.md) 每个请求。

 

