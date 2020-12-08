---
title: 微型驱动程序同步
description: 微型驱动程序同步
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，同步
- 流式处理微型驱动程序 WDK Windows 2000 内核，同步
- 微型驱动程序 WDK Windows 2000 内核流式处理，同步
- 同步 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f91535264d4a972e42a84552ff43a3fdd60c859
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833265"
---
# <a name="minidriver-synchronization"></a>微型驱动程序同步





流式处理微型驱动程序开发人员可以选择允许类驱动程序处理同步。 当微型驱动程序向类驱动程序注册自身时，它们可以通过将 [**HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)的 **TurnOffSynchronization** 成员设置为 **FALSE** 来选择提供类驱动程序同步。

当类驱动程序处理同步时，它将确保两个微型驱动程序代码段永远不会同时执行。 类驱动程序将所有流请求排队，并一次将这些请求传递给微型驱动程序。

此同步的一个目的是让微型驱动程序编写人员在多任务、可重入的多处理器环境中处理驱动程序同步和请求队列的所有详细信息。 但有些微型驱动程序不应使用它。 [同步示例](synchronization-examples.md)主题中提供了两个示例，演示了微型驱动程序需要执行哪些操作来与同步有关。

禁用流类同步意味着所有请求都立即和异步调用到被动级别的提交线程上下文中的微型驱动程序 \_ 。 上述规则的例外是 HwCancelPacket、TimeoutHandler 和 Timer 例程。 这些是在调度级别调用的 \_ 。 最后一个例外是中断处理程序，它在 DIRQL 调用。

当同步关闭时，微型驱动程序负责执行与 WDM 模型相容的同步。 如果在被动级别调用了微型驱动程序 \_ ，则它可以被任何更高的 IRQL 事件（例如 dpc 或中断）抢占。 同样，如果在调度级别回调了微型驱动程序 \_ ，则它可能会被中断抢占。 操作共享资源的微型驱动程序函数必须同步访问。

流类同步关闭时，可以将多个请求同时发送到相同或不同的流。 微型驱动程序必须将自己的请求排队，并处理与其他线程和 ISR 的任何硬件同步。 自旋锁、mutex 和 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution) 是一些同步对象，可用于 stream 微型驱动程序运行，而无需流类同步。

 

