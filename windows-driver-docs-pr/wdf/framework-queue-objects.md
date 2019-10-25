---
title: 框架队列对象
description: 框架队列对象
ms.assetid: 42736e2d-2482-46b4-bf52-4efe369db40b
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
ms.openlocfilehash: 69da8ea24232dfc28af6626d6e7e843395090692
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845134"
---
# <a name="framework-queue-objects"></a>框架队列对象





框架队列对象表示*i/o 队列*，这些队列是驱动程序接收的 i/o 请求的容器。 每个驱动程序都可以为每个设备创建一个或多个 i/o 队列。 框架队列对象定义一组[事件回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/)，驱动程序可以提供该函数，以及驱动程序可调用的一组对象方法。

当框架收到定向到某个驱动程序设备的 i/o 请求时，框架会将该请求放入相应的 i/o 队列。 如果你的驱动程序注册一个或多个[请求处理程序](request-handlers.md)，则每次出现 i/o 请求时，框架都可以通知你的驱动程序。 或者，你的驱动程序可以轮询请求的 i/o 队列。

本部分包括：

[创建 i/o 队列](creating-i-o-queues.md)

[删除 i/o 队列](deleting-i-o-queues.md)

[管理 i/o 队列](managing-i-o-queues.md)

[使用电源托管 i/o 队列](using-power-managed-i-o-queues.md)

[保证 i/o 操作的前进进度](guaranteeing-forward-progress-of-i-o-operations.md)

[I/o 队列状态](i-o-queue-states.md)

[I/o 队列的示例用法](example-uses-of-i-o-queues.md)

 

 





