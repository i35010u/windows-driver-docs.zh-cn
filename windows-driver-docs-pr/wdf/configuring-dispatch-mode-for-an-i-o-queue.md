---
title: 为 I/O 队列配置调度模式
description: 为 I/O 队列配置调度模式
ms.assetid: 7603c3fd-a4cb-4174-ad14-f57efedfe9de
keywords:
- 同步 WDK UMDF
- 队列调度模式 WDK UMDF
- 调度模式 WDK UMDF
- I/o 队列 WDK UMDF
- 队列 WDK UMDF
- 顺序调度模式 WDK UMDF
- 并行调度模式 WDK UMDF
- 手动调度模式 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f09c0c4bda351144b1469778101523896b8ba907
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843646"
---
# <a name="configuring-dispatch-mode-for-an-io-queue"></a>为 I/O 队列配置调度模式


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

当应用程序的 i/o 请求到达时，框架会将每个请求放入相应的 i/o 队列。 请求传递到驱动程序的方式和时间取决于驱动程序如何为 i/o 队列配置调度以及驱动程序如何[指定回叫功能同步](specifying-a-callback-synchronization-mode.md)。 I/o 队列还与 UMDF 的 PnP 和电源管理子系统交互，以便在设备达到正确状态之前在队列中保存 i/o 请求。

**请注意**   I/o 队列的调度模式与[同步模式](specifying-a-callback-synchronization-mode.md)无关。 I/o 队列的调度配置控制驱动程序可在任何给定时间处理的请求数，同时同步控制呈现或取消请求的事件回调函数的同时执行。 但是，多个操作模式是通过[组合调度和同步模式](combining-dispatch-and-synchronization-modes.md)来创建的。

 

当驱动程序调用[**IWDFDevice：： CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)方法来配置默认队列或创建辅助队列时，驱动程序会为 i/o 队列配置调度。 驱动程序可以在**IWDFDevice：： CreateIoQueue**的*DispatchType*参数中指定一个来自[**WDF\_IO\_QUEUE\_调度\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ne-wdfio-_wdf_io_queue_dispatch_type)枚举类型的值，以标识调度模式。 [I/o 队列对象](framework-i-o-queue-object.md)可支持以下调度模式：

-   连续性

    使用**WdfIoQueueDispatchSequential**值指定顺序调度模式。 在此调度模式下，处于处理状态的队列将引发事件，以便驱动程序一次只处理一个请求。 队列会推迟任何其他请求，直到驱动程序完成其当前请求的处理，或调用[**IWDFIoRequest：： ForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-forwardtoioqueue)方法来重新排队请求。 当前请求完成或转发后，队列将引发一个事件以提供下一个请求。

-   并行

    并行调度模式使用**WdfIoQueueDispatchParallel**值指定。 在此调度模式下，处理状态中的队列会在 i/o 请求为驱动程序准备就绪后引发事件。 当驱动程序收到 i/o 请求时，驱动程序可以通过以下方式之一来处理 i/o 请求：

    -   驱动程序调用[**IWDFIoRequest：： Complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)或[**IWDFIoRequest：： CompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)方法立即完成 i/o 请求。 如果 i/o 请求无效、无法进行处理，则驱动程序会立即完成 i/o 请求，或者可以通过从包含数据的缓冲区或缓存复制数据来完成该请求。
    -   驱动程序调用[**IWDFIoRequest：： ForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-forwardtoioqueue)方法来重新排队 i/o 请求。
    -   驱动程序调用[**IWDFIoRequest：： Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)方法将 i/o 请求传递到较低级别的驱动程序。
-   Manual

    手动调度模式使用**WdfIoQueueDispatchManual**值指定。 在此调度模式下，当请求到达队列时，i/o 队列不会自动通知驱动程序。 驱动程序必须调用[**IWDFIoQueue：： RetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfioqueue-retrievenextrequest)方法，以便从队列中手动检索请求。 这是一个轮询模型。

    在 UMDF 版本1.9 及更高版本中，如果驱动程序使用手动调度模式，则它可以调用[**IWDFIoRequest2：：重新排队**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-requeue)将 i/o 请求返回到从中获取驱动程序的 i/o 队列的开头。 调用**IWDFIoRequest2：：重新排队**之后，驱动程序对[**IWDFIoQueue：： RetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfioqueue-retrievenextrequest)的下一次调用将检索重新排队的请求。

对于所有调度模式， [i/o 队列对象](framework-i-o-queue-object.md)会接收并跟踪请求，直到驱动程序处理请求或取消请求。

如果驱动程序将队列配置为使用串行或并行调度，则当驱动程序创建队列或配置默认队列时，框架会通过驱动程序注册的回调函数通知请求的驱动程序。 有关详细信息，请参阅[I/o 队列事件回调函数](i-o-queue-event-callback-functions.md)。

 

 





