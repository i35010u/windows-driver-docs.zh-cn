---
title: 框架队列对象
description: 框架队列对象
keywords:
- I/o 请求 WDK KMDF，队列对象
- I/o 队列 WDK KMDF
- 队列对象 WDK KMDF
- I/o 队列对象 WDK KMDF
- 请求处理 WDK KMDF，队列对象
- 队列 WDK KMDF
- 队列 WDK KMDF，框架对象
- I/o 队列 WDK KMDF，关于 i/o 队列
- 回调函数 WDK KMDF
- 事件回调函数 WDK KMDF
- framework 对象 WDK KMDF、i/o 队列对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b34dfabd7f25171fe6956dd2e22d3f953a59dc6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814767"
---
# <a name="framework-queue-objects"></a>框架队列对象





框架队列对象表示 *i/o 队列*，这些队列是驱动程序接收的 i/o 请求的容器。 每个驱动程序都可以为每个设备创建一个或多个 i/o 队列。 框架队列对象定义一组 [事件回调函数](/windows-hardware/drivers/ddi/wdfio/) ，驱动程序可以提供该函数，以及驱动程序可调用的一组对象方法。

当框架收到定向到某个驱动程序设备的 i/o 请求时，框架会将该请求放入相应的 i/o 队列。 如果你的驱动程序注册一个或多个 [请求处理程序](request-handlers.md)，则每次出现 i/o 请求时，框架都可以通知你的驱动程序。 或者，你的驱动程序可以轮询请求的 i/o 队列。

本节包括：

[创建 I/O 队列](creating-i-o-queues.md)

[删除 I/O 队列](deleting-i-o-queues.md)

[管理 I/O 队列](managing-i-o-queues.md)

[使用通过电源管理的 I/O 队列](using-power-managed-i-o-queues.md)

[保证向前推进 I/O 操作](guaranteeing-forward-progress-of-i-o-operations.md)

[I/O 队列状态](i-o-queue-states.md)

[I/O 队列的示例使用](example-uses-of-i-o-queues.md)

 

