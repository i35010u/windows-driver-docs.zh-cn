---
title: 框架队列对象
description: 框架队列对象
ms.assetid: 42736e2d-2482-46b4-bf52-4efe369db40b
keywords:
- I/O 请求 WDK KMDF，队列对象
- WDK KMDF 的 I/O 队列
- 队列对象 WDK KMDF
- I/O 队列对象 WDK KMDF
- 请求处理 WDK KMDF，队列对象
- 队列 WDK KMDF
- 队列 WDK KMDF，framework 对象
- 有关 I/O 队列的 I/O 队列 WDK KMDF
- 回调函数 WDK KMDF
- 事件回调函数 WDK KMDF
- framework 对象 WDK KMDF，I/O 队列对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c91318ab44cfd0bbb76e78e91d51a87f98b534d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384453"
---
# <a name="framework-queue-objects"></a>框架队列对象





Framework 队列对象表示*I/O 队列*，这是 I/O 的容器，驱动程序收到的请求。 每个驱动程序可以创建一个或多个 I/O 队列用于每个设备。 Framework 队列对象定义一组[事件的回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/)可提供驱动程序和驱动程序可以调用的对象方法的一组。

当框架接收定向到一个驱动程序的设备的 I/O 请求时，该框架会将请求放置在相应的 I/O 队列。 如果您的驱动程序将注册一个或多个[请求处理程序](request-handlers.md)，框架可以通知您的驱动程序每次 I/O 请求时可用。 或者，您的驱动程序可以轮询请求的 I/O 队列。

本部分包括：

[创建的 I/O 队列](creating-i-o-queues.md)

[删除 I/O 队列](deleting-i-o-queues.md)

[管理 I/O 队列](managing-i-o-queues.md)

[使用电源管理的 I/O 队列](using-power-managed-i-o-queues.md)

[保证向前推进的 I/O 操作](guaranteeing-forward-progress-of-i-o-operations.md)

[I/O 队列状态](i-o-queue-states.md)

[示例使用的 I/O 队列](example-uses-of-i-o-queues.md)

 

 





