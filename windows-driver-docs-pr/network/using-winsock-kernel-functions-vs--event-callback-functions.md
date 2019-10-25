---
title: 使用 Winsock 内核函数与事件回调函数
description: 使用 Winsock 内核函数与
ms.assetid: 63a3f933-f74a-4cb8-a7a9-9498e1c17afa
keywords:
- Winsock 内核 WDK 网络，函数
- WSK WDK 网络，函数
- Winsock 内核 WDK 网络，事件
- WSK WDK 网络，事件
- 事件 WDK Winsock 内核
- 函数 WDK Winsock 内核
- 事件回调函数 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dff14c922cd564294d5dee0639258bb0ba6152fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842962"
---
# <a name="using-winsock-kernel-functions-vs-event-callback-functions"></a>使用 Winsock 内核函数与事件回调函数


对于某些套接字操作，Winsock 内核（WSK）应用程序可以调用某个套接字的 WSK 函数来执行操作，或在该[事件发生](winsock-kernel-events.md)时 WSK 子系统调用的套接字上实现和启用事件回调函数。发生与操作关联的。 例如，在面向连接的套接字上接收数据时，WSK 应用程序可以调用套接字的[**WskReceive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive)函数，或在套接字上实现和启用[*WskReceiveEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_receive_event)事件回调函数。 WSK 应用程序的要求规定了应用程序应该使用哪种方法。 WSK 文档中提供了有关如何使用这两种方法的示例。

下面的列表总结了每种方法的一些要点。

### <a name="using-winsock-kernel-functions"></a>使用 Winsock 内核函数

-   WSK 应用程序驱动套接字操作，这意味着 WSK 应用程序控制何时发生套接字操作。 这可以简化 WSK 应用程序所需的同步。

-   WSK 应用程序为套接字函数提供 Irp。 这些 Irp 会按 WSK 子系统排队，直到套接字操作完成。 有关将 Irp 用于 WSK 函数的详细信息，请参阅将[irp 与 Winsock 内核函数结合使用](using-irps-with-winsock-kernel-functions.md)。

-   WSK 应用程序可通过等待 WSK 子系统完成每个操作的 IRP 来执行阻塞套接字操作。

-   WSK 应用程序可能需要在某些情况下使多个套接字操作排队，以确保面向连接的套接字上的高性能数据传输，以防传入的数据报在数据报套接字上被丢弃，或防止正在侦听插槽上丢弃的传入连接。

-   WSK 应用程序提供数据传输操作的数据缓冲区。 这减少了可能需要复制数据的次数。 但是，如果 WSK 应用程序将多个数据传输操作排入队列，则该应用程序必须为每个排队数据传输操作的 WSK 子系统提供数据缓冲区。 因此，WSK 应用程序可能需要额外的内存资源。

### <a name="using-event-callback-functions"></a>使用事件回调函数

-   WSK 子系统驱动套接字操作，这意味着 WSK 子系统通过调用套接字的事件回调函数通知 WSK 应用套接字的事件。 WSK 应用程序可能需要更复杂的同步来处理事件回调函数的异步特性。

-   WSK 应用程序不使用 Irp 来执行套接字操作。

-   WSK 应用程序不需要对套接字操作进行排队。 当套接字的事件发生时，WSK 子系统会立即调用 WSK 应用程序的事件回调函数。 如果 WSK 应用程序可以跟上套接字事件回调函数的调用速率，使用事件回调函数可以提供最高的性能和丢弃数据报或传入连接的最小机会。

-   WSK 子系统提供数据缓冲区用于数据传输操作。 WSK 应用程序必须立即或在合理的时间内将这些数据缓冲区释放回 WSK 子系统，以便 WSK 子系统不会用尽内存资源。 因此，WSK 应用程序可能需要将数据从 WSK 子系统拥有的数据缓冲区复制到其自己的数据缓冲区。

**请注意**，  以上列表并不一定详尽。 选择哪种方法是特定 WSK 应用程序的最佳选择时，可能需要考虑其他一些事项。

 

 

 





