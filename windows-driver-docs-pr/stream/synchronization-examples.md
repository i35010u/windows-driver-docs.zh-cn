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
ms.openlocfilehash: 7b2462e67bd0be2cf47ed539283cbeb291cf8a21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564732"
---
# <a name="synchronization-examples"></a>同步示例





下面的示例演示了需要做些同步的微型驱动程序，包括时应不使用同步的示例：

-   **示例 1:与正常运行 ISR 微型驱动程序**

    如果流类同步功能在所有微型驱动程序入口点在引发 IRQL 调用，使用[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)，这意味着，在适配器和所有较低的 IRQ 的 IRQ 级别微型驱动程序执行其代码时，会屏蔽级别。 因此，它是命令性微型驱动程序做仅种小型的大量，在此模式下工作。

    微型驱动程序不应运行代码，通常用来引发 IRQL 在多个 10 到 20 毫秒。 如果使用的调试版本*stream.sys*，stream 类记录在引发 IRQL 所用的时间量和断言如果驱动程序花费时间过长。 如果微型驱动程序只是需要程序硬件 DMA 注册请求，或只需读取其 ISR 中的端口，则通常可以执行所有引发的 IRQL 在其处理操作。

    如果微型驱动程序需要执行时间超过几微秒为单位的处理，如将通过 PIO，微型驱动程序的数据传输的微型驱动程序应使用[ **StreamClassCallAtNewPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff568230)到计划调度\_级别回调。 在回调中，微型驱动程序可能需要最多 1/2 到 1 毫秒周围以进行处理。 有一点需要记住何时在此模式下是调度\_级别回调*不*ISR 与同步

    这种同步的缺乏不是问题，如果硬件微型驱动程序回调以及如下所示 ISR 期间访问资源 （例如，端口或队列） 时保持不变 但如果不稳定可能是个问题，必须使用微型驱动程序**StreamClassCallAtNewPriority**安排高优先级回调的调度\_级别回调涉及与共享的资源使用 ISR 的资源

    请注意，高优先级回调是等效于调用**KeSynchronizeExecution**。 **KeSynchronizeExecution**需要微型驱动程序可以引用多个参数的[ **StreamClassCallAtNewPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff568230)没有相同的行为中的两个结果，但一般情况下。

    如果微型驱动程序只是偶尔需要运行代码花费更多比 1/2 到 1 毫秒，或偶尔需要调用服务在被动\_级别 (如在初始化时)，然后设置**StreamClassCallAtNewPriority**为低优先级可用于获取一种被动\_级别工作线程。 请注意，低优先级回调不会同步使用的任何内容，微型驱动程序才能接收新的请求 (假设**ReadyForNextRequest** NotificationType 参数处于挂起状态) 或运行较低时的 ISR 调用优先级的回调。

-   **示例二：而无需 ISR 微型驱动程序**

    如果开启流类同步，微型驱动程序的入口点所有在调用调度\_级别。 微型驱动程序可以执行操作的最多处理围绕 1/2 到 1 毫秒持续时间而无需调整优先级。 如果微型驱动程序只是偶尔需要运行代码，需要使用多个 1/2 毫秒或偶尔需要调用服务在被动\_级别 (如在初始化时)，然后[ **StreamClassCallAtNewPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff568230)与低优先级可用于获取一种被动\_级别工作线程。 请注意，低优先级回调不与任何内容同步，微型驱动程序可能会收到新的请求 (假设**ReadyForNextRequest** NotificationType 参数处于挂起状态) 时运行的低优先级回调。

-   **Stream 类同步应在何时*****不*****是使用**

    以下是其中流类同步不应使用的情况的示例。 这些问题包括：

    -   驱动程序频繁地 （超过大约 20%的微型驱动程序收到的请求) 需要执行时间超过 1 毫秒的处理或需要频繁地调用被动\_级服务，如 Microsoft DirectDraw 服务。 使用的调试版本时*stream.sys*、 流类将添加这两种情况，并停止，如果检测到同步打开上。
    -   微型驱动程序时没有相关联的硬件的筛选器。 这种微型驱动程序应运行在被动\_级别由于无需与同步的基础硬件，并且微型驱动程序通常执行大量的处理。 它是更轻松地在这种情况下比要浪费开销使用执行你自己的同步流类同步。 如有必要，使用互斥体，以保护您的队列。

        同步代码中的 bug 可能通常很难查找，并在某些环境中 （例如基于 NT 的操作系统在多处理器系统上运行） bug 可能会显示仅在压力的很多时间之后。 根据与供应商的经验，这些是不了几种大多数供应商具有的功能，或希望调试。 仅驱动程序编写人员熟悉编写完全异步的 WDM 设备驱动程序应尝试执行其自己的同步。

    -   微型驱动程序时的总线上总线类型驱动程序 （例如，USB 或 1394年外围设备驱动程序），实际上却不担心同步实际硬件，但只需调用到下一层的请求的被动\_级别，并接收通常在调度回调\_级别。

 

 




