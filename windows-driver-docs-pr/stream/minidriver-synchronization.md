---
title: 微型驱动程序同步
description: 微型驱动程序同步
ms.assetid: 2f560e7a-4717-4b3f-9513-e34fcb2b5e6c
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，同步
- 流式处理微型驱动程序 WDK Windows 2000 内核，同步
- 微型驱动程序 WDK Windows 2000 内核流式处理，同步
- 同步 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f790ce83603ffe974e670073e93426509894414
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567204"
---
# <a name="minidriver-synchronization"></a>微型驱动程序同步





流式处理的微型驱动程序开发人员可以选择允许在类驱动程序，以处理同步。 当微型驱动程序注册自己的类驱动程序时，他们可以通过设置选择类驱动程序提供同步**TurnOffSynchronization**的成员[ **HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff559682)到**FALSE**。

当在类驱动程序处理同步时，它可确保永远不会同时执行两条微型驱动程序代码。 类驱动程序排队所有的流请求，并一次将其传递给微型驱动程序之一。

此同步的一个用途是备用的微型驱动程序编写器无需处理驱动程序同步和多处理器环境中的多任务，可重入，队列的请求的所有详细信息。 但是，某些微型驱动程序不应使用它。 中提供了两个示例[同步示例](synchronization-examples.md)说明需要执行涉及同步的微型驱动程序的主题。

打开流类同步关闭状态的所有请求会立即以异步方式都调用和向下到被动提交线程的上下文中微型驱动程序的表示\_级别。 上述规则的例外情况是 HwCancelPacket、 TimeoutHandler 和计时器的例程。 这些在调度调用\_级别。 一个最终异常是在 DIRQL 调用的中断处理程序。

如果关闭了同步，微型驱动程序负责执行符合 WDM 模型同步。 如果在被动回调用微型驱动程序\_级别，然后可以通过任何更高版本的 IRQL 事件，如 Dpc 或中断抢占它。 同样，如果在调度回调用微型驱动程序\_级别，它可以随后会被抢占的中断。 操作共享的资源的微型驱动程序函数必须同步访问。

流类同步处于关闭状态时，可以向相同或不同流同时发出多个请求。 微型驱动程序必须对其自己的请求进行排队和处理与其他线程和 ISR 任何硬件同步 旋转锁，互斥体，并[ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)是一些同步对象可用于流微型驱动程序无需进行流类同步运行。

 

 




