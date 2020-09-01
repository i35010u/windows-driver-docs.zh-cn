---
title: 同步示例
description: 同步示例
ms.assetid: b9290fab-8213-4083-bda5-0e6c2af737a6
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，同步
- 流式处理微型驱动程序 WDK Windows 2000 内核，同步
- 微型驱动程序 WDK Windows 2000 内核流式处理，同步
- 同步 WDK 流式处理微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b039c6643f3e9f126c0de92d470ce07f1d06fb7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189925"
---
# <a name="synchronization-examples"></a>同步示例





下面的示例说明了微型驱动程序需要执行哪些操作来实现同步，并包含同步不应使用的示例：

-   **示例一：具有正常运行的 ISR 的微型驱动程序**

    如果启用了流类同步，则会在使用 KeSynchronizeExecution 的情况下，使用[**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)调用所有微型驱动程序入口点，这意味着在微型驱动程序执行其代码时，会屏蔽适配器的 irq 级别和所有较低的 irq 级别。 因此，在此模式下，微型驱动程序只能执行少量的工作。

    微型驱动程序不应运行通常会超过10到20微秒的代码，产生的 IRQL。 如果使用 *stream.sys*的调试版本，则如果驱动程序在该驱动程序中花费了太长时间，则该 stream 类会记录产生 IRQL 和断言所用的时间。 如果微型驱动程序只需为请求计划硬件 DMA 注册，或只需读取其 ISR 中的端口，则通常可以接受所有处理，并引发 IRQL。

    如果微型驱动程序需要执行的处理操作所需的时间超过几微秒，如通过 PIO 传输数据的微型驱动程序，则微型驱动程序应使用 [**StreamClassCallAtNewPriority**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclasscallatnewpriority) 来计划调度 \_ 级别回调。 在回调中，微型驱动程序最多可能需要1/2 到1毫秒才能完成处理。 在此模式下需要记住的一点是，调度 \_ 级别回调 *不* 与 ISR 同步。

    如果在微型驱动程序访问资源时硬件保持稳定，则这种不同步的情况并不是个问题 (例如，在回调和 ISR 中) 的端口或队列。 但如果不稳定可能是一个问题，则微型驱动程序必须使用 **StreamClassCallAtNewPriority** 来计划高优先级回拨，其中调度 \_ 级别回调涉及与 ISR 使用的资源共享的资源。

    请注意，高优先级回调等效于调用 **KeSynchronizeExecution**。 **KeSynchronizeExecution** 要求微型驱动程序引用 [**StreamClassCallAtNewPriority**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclasscallatnewpriority) 不具有的多个参数，但通常情况下，这两个参数会导致相同的行为。

    如果微型驱动程序只是偶尔需要运行超过1/2 到1毫秒的代码，或者偶尔需要在被动级别调用服务 \_ (如在初始化时) ，则将 **StreamClassCallAtNewPriority** 设置为低优先级可用于获取被动 \_ 级别工作线程。 请注意，低优先级回叫不会与任何内容同步，并且微型驱动程序可能会收到新请求， (假设 **ReadyForNextRequest** NotificationType 参数处于挂起) 状态，或者运行低优先级回调时，ISR 调用。

-   **示例2：不带 ISR 的微型驱动程序**

    如果打开流类同步，则微型驱动程序的入口点都在调度 \_ 级别调用。 微型驱动程序可以处理大约1/2 到1毫秒的时间，而无需调整优先级。 如果微型驱动程序偶尔只需要运行超过1/2 毫秒的代码，或者偶尔需要在被动级别调用服务 \_ (如在初始化时) ，则可以使用低优先级的 [**STREAMCLASSCALLATNEWPRIORITY**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclasscallatnewpriority) 获取被动 \_ 级别的工作线程。 请注意，低优先级回叫不会与任何内容同步，微型驱动程序可能会收到新请求， (假设 **ReadyForNextRequest** NotificationType 参数在运行低优先级回调时挂起) 。

-   **_不_** 应**使用****流类同步的时间**

    下面是不应使用流类同步的情况的示例。 这些方法包括：

    -   当驱动程序经常 (超过20% 的请求数时，微型驱动程序收到的请求) 需要执行的处理需要超过1毫秒，或者需要频繁调用被动 \_ 级服务，如 Microsoft DirectDraw 服务。 使用 *stream.sys*的调试版本时，如果在启用了同步的情况下检测到它们，则 stream 类将断言这两种情况并停止。
    -   如果微型驱动程序是没有关联硬件的筛选器，则为。 此类微型驱动程序应在被动级别运行 \_ ，因为没有要与之同步的基础硬件，并且微型驱动程序通常会执行大量处理。 在这种情况下，你可以更轻松地执行自己的同步，而不是使用流类同步浪费开销。 如有必要，请使用 mutex 来保护队列。

        同步代码中的 bug 通常很难查找，在某些环境中 (例如，在多处理器系统上运行的基于 NT 的操作系统) bug 可能会在几小时后出现。 根据供应商的经验，这些功能并不是大多数供应商对其进行调试的功能。 只有熟悉编写完全异步的 WDM 设备驱动程序的驱动程序编写人员才能尝试执行其自己的同步。

    -   如果微型驱动程序是总线上总线类型的驱动程序 (例如，USB 或1394外设驱动程序) 不必真正担心实际硬件的同步，而只是将请求向下发送到被动级别的下一层， \_ 并且通常在调度级别接收回调 \_ 。

 

