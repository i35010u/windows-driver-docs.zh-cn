---
title: 框架 I/O 队列对象
description: 框架 I/O 队列对象
ms.assetid: b343c61a-8252-4e46-9013-bef29d9ec360
keywords:
- UMDF 对象 WDK，I/O 队列对象
- framework 对象 WDK UMDF，I/O 队列对象
- I/O 队列对象 WDK UMDF
- IWDFIoQueue
- 队列对象 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93db224fe5a7b912130f745a2a1d49d23d73add5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373723"
---
# <a name="framework-io-queue-object"></a>框架 I/O 队列对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Framework I/O 队列对象公开到由驱动程序[IWDFIoQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfioqueue)接口。 它表示的 I/O 队列，这是 I/O 请求的容器。 I/O 队列到驱动程序控制请求的流。 当 I/O 请求到达时，它被放在相应的队列。 I/O 队列对象是的子级[UMDF 设备对象](framework-device-object.md)。 驱动程序可以调用[ **IWDFDevice::CreateIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)方法来创建 I/O 队列对象。 在调用**IWDFDevice::CreateIoQueue**，驱动程序可以指定队列是默认的队列。

该驱动程序创建一个 I/O 队列，它指定控制请求传递到驱动程序的调度模型。 有关详细信息，请参阅[I/O 队列配置调度模式](configuring-dispatch-mode-for-an-i-o-queue.md)。

当驱动程序创建的 I/O 队列时，他们可以与框架相关的接口的事件发生时通知该驱动程序调用的回调函数提供接口。 有关详细信息，请参阅[I/O 队列事件回调函数](i-o-queue-event-callback-functions.md)。

 

 





