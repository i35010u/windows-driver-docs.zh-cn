---
title: 框架 I/O 队列对象
description: 框架 I/O 队列对象
keywords:
- UMDF 对象 WDK，i/o 队列对象
- framework 对象 WDK UMDF，i/o 队列对象
- I/o 队列对象 WDK UMDF
- IWDFIoQueue
- 队列对象 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8301e6abefadc11e8c91cadd31dee591e3c2dbef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815711"
---
# <a name="framework-io-queue-object"></a>框架 I/O 队列对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架 i/o 队列对象由 [IWDFIoQueue](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfioqueue) 接口公开给驱动程序。 它表示 i/o 队列，这是 i/o 请求的容器。 I/o 队列控制传入驱动程序的请求流。 当 i/o 请求到达时，它将被置于适当的队列中。 I/o 队列对象是 [UMDF 设备对象](framework-device-object.md)的子项。 驱动程序可以调用 [**IWDFDevice：： CreateIoQueue**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue) 方法来创建 i/o 队列对象。 在对 **IWDFDevice：： CreateIoQueue** 的调用中，驱动程序可以指定队列是否为默认队列。

当驱动程序创建 i/o 队列时，它将指定一个调度模型，该模型控制向驱动程序发出请求的传送。 有关详细信息，请参阅为 [I/o 队列配置调度模式](configuring-dispatch-mode-for-an-i-o-queue.md)。

当驱动程序创建 i/o 队列时，它们可以为该框架所调用的回调函数提供接口，以便在与接口相关的事件发生时通知驱动程序。 有关详细信息，请参阅 [I/o 队列事件回调函数](i-o-queue-event-callback-functions.md)。

 

