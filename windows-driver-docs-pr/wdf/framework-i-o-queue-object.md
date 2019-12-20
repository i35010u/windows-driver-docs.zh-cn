---
title: 框架 I/O 队列对象
description: 框架 I/O 队列对象
ms.assetid: b343c61a-8252-4e46-9013-bef29d9ec360
keywords:
- UMDF 对象 WDK，i/o 队列对象
- framework 对象 WDK UMDF，i/o 队列对象
- I/o 队列对象 WDK UMDF
- IWDFIoQueue
- 队列对象 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64cca126dd69a87e07b81998ad5453db0402f908
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210413"
---
# <a name="framework-io-queue-object"></a>框架 I/O 队列对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架 i/o 队列对象由[IWDFIoQueue](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfioqueue)接口公开给驱动程序。 它表示 i/o 队列，这是 i/o 请求的容器。 I/o 队列控制传入驱动程序的请求流。 当 i/o 请求到达时，它将被置于适当的队列中。 I/o 队列对象是[UMDF 设备对象](framework-device-object.md)的子项。 驱动程序可以调用[**IWDFDevice：： CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)方法来创建 i/o 队列对象。 在对**IWDFDevice：： CreateIoQueue**的调用中，驱动程序可以指定队列是否为默认队列。

当驱动程序创建 i/o 队列时，它将指定一个调度模型，该模型控制向驱动程序发出请求的传送。 有关详细信息，请参阅为[I/o 队列配置调度模式](configuring-dispatch-mode-for-an-i-o-queue.md)。

当驱动程序创建 i/o 队列时，它们可以为该框架所调用的回调函数提供接口，以便在与接口相关的事件发生时通知驱动程序。 有关详细信息，请参阅[I/o 队列事件回调函数](i-o-queue-event-callback-functions.md)。

 

 





