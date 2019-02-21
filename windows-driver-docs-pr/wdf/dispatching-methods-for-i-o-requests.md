---
title: I/O 请求的调度方法
description: I/O 请求的调度方法
ms.assetid: 3e91aa7c-bccf-4eeb-8b68-b1277a690f8c
keywords:
- I/O 队列 WDK KMDF，创建
- I/O 队列 WDK KMDF，调度方法
- 调度方法 WDK KMDF
- 顺序调度 WDK KMDF
- 同步调度 WDK KMDF
- 并行调度 WDK KMDF
- 异步调度 WDK KMDF
- 手动调度 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 191ff93f32acfb5e757da2253a678c8cdff1cfe9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525991"
---
# <a name="dispatching-methods-for-io-requests"></a>I/O 请求的调度方法





当驱动程序调用[ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)若要创建的 I/O 队列，它指定队列的调度方法。 该框架提供了三个调度方法：[顺序](#sequential-dispatching)，[并行](#parallel-dispatching)，并[手动](#manual-dispatching)。 该驱动程序可以指定其中的任何调度的任何 I/O 队列，包括设备的方法[默认 I/O 队列](creating-i-o-queues.md)。

驱动程序设置队列的调度方法通过指定[ **WDF\_IO\_队列\_调度\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff552362)-队列中的类型的值[**WDF\_IO\_队列\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)结构。

有关示例使用的每个调度的方法，请参阅[I/O 队列的示例使用](example-uses-of-i-o-queues.md)。

### <a href="" id="sequential-dispatching"></a> 顺序调度

如果您的驱动程序或设备可以处理一次只有一个 I/O 请求从队列，则应设置设备的 I/O 队列用于*顺序调度*，这也称为*同步调度*。 使用此类型的调度，框架提供的请求向一个驱动程序一次。 框架并不提供驱动程序直到下一个请求[完成](completing-i-o-requests.md)，[取消](canceling-i-o-requests.md)，或[requeues](requeuing-i-o-requests.md)上一个请求。

该框架将请求传递到一个驱动程序的后[请求处理程序](request-handlers.md)，该驱动程序[处理请求](processing-i-o-requests.md)。 如果该驱动程序将请求转发到[常规 I/O 目标](general-i-o-targets.md)，它通常会调用一个 I/O 目标对象的同步方法。 有关这些方法的详细信息，请参阅[以同步方式发送 I/O 请求](sending-i-o-requests-synchronously.md)。 该驱动程序必须最终[完整](completing-i-o-requests.md)或[取消](canceling-i-o-requests.md)I/O 队列中收到的每个请求。

设置了 I/O 队列的顺序调度可以调用的驱动程序[ **WdfIoQueueRetrieveNextRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548462)或[ **WdfIoQueueRetrieveRequestByFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548470)从早于最后队列获取另一个请求收到的请求已完成或已取消。 您可能想要执行此操作到函数的驱动程序，以便驱动程序可以开始时，驱动程序的下一个硬件操作[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)回调函数仍在处理从以前的数据硬件操作。

如果创建多个 I/O 队列并将它们设置所有最多的顺序调度，框架会将请求分派从每个队列按顺序，但队列以并行方式运行。 如果驱动程序或设备可以处理任何类型的一次只有一个请求，则必须使用与单个 I/O 队列[ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)回调函数。

### <a href="" id="parallel-dispatching"></a> 并行调度

如果您的驱动程序和设备可以同时处理多个 I/O 请求，则可以设置设备的 I/O 队列用于*并行调度*以便驱动程序可以以异步方式处理请求。 此调度方法也称为*异步调度*。

如果驱动程序设置的 I/O 队列，以使用并行调度，框架提供给驱动程序 I/O 请求的只要它们是在队列中可用。 结果是驱动程序可能需要在一次处理多个请求。

每次在驱动程序之一[请求处理程序](request-handlers.md)收到请求时，该驱动程序必须[处理该请求](processing-i-o-requests.md)，然后[完整](completing-i-o-requests.md)请求。 如果该驱动程序将请求转发到[常规 I/O 目标](general-i-o-targets.md)，它通常会调用一个 I/O 目标对象的异步方法。 有关这些方法的详细信息，请参阅[以异步方式发送 I/O 请求](sending-i-o-requests-asynchronously.md)。 该驱动程序必须最终[完整](completing-i-o-requests.md)或[取消](canceling-i-o-requests.md)I/O 队列中收到的每个请求。

使用并行调度的驱动程序可以调用[ **WdfIoQueueStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548482)或[ **WdfIoQueueStopSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548489)若要暂时停止队列，然后再调用[ **WdfIoQueueStart** ](https://msdn.microsoft.com/library/windows/hardware/ff548478)重新启动队列。

### <a href="" id="manual-dispatching"></a> 手动调度

如果您希望您可以完全控制的 I/O 请求传递的驱动程序，您可以设置设备的 I/O 队列用于*手动调度*，这意味着，该框架不请求向传递该驱动程序除非驱动程序明确要求之一。

若要获取从手动队列请求，该驱动程序可以调用[ **WdfIoQueueRetrieveNextRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548462)或[ **WdfIoQueueRetrieveRequestByFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548470)轮询队列中的循环中。 或者，驱动程序可以调用[ **WdfIoQueueReadyNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff548452)注册一个或多个请求在队列中可用时，框架将调用的回调函数。 该驱动程序框架调用的回调函数后，可以调用**WdfIoQueueRetrieveNextRequest**或**WdfIoQueueRetrieveRequestByFileObject**中用于检索请求的循环。

驱动程序将从队列获取请求后，它必须[处理该请求](processing-i-o-requests.md)。 该驱动程序必须最终[完整](completing-i-o-requests.md)或[取消](canceling-i-o-requests.md)每个请求。

 

 





