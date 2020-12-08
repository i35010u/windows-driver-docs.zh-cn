---
title: 调试会话和执行模型
description: 调试会话和执行模型
keywords:
- 调试器引擎，执行模型
- 执行模型
- 调试器引擎，调试会话
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f3a0bc6de3e11f486b5bd5d0789cae4609343cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839803"
---
# <a name="debugging-session-and-execution-model"></a>调试会话和执行模型


调试器引擎可以同时调试多个目标。 当引擎获取目标并继续，直到放弃所有目标时， *调试会话* 即开始。 当目标在运行时 *无法* 访问，并且在当前目标挂起时 *可访问* 调试会话。 该引擎只能用于在会话可访问时检查和操作目标。

调试器的主循环通常包括设置执行状态、调用方法 [**WaitForEvent**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-waitforevent) 和处理生成的 [事件](events.md#events)。 调用 **WaitForEvent** 时，会话将无法访问。

当目标中发生事件时，引擎将挂起所有目标，并且会话将可供访问。 然后，引擎会通知事件的事件回调并遵循事件筛选规则。 事件回调和事件筛选器确定如何继续执行目标中的执行。 如果它们确定引擎应中断到调试器中，则 **WaitForEvent** 方法将返回，并且会话仍可访问;否则，引擎将以事件回调和事件筛选器确定的方式恢复目标的执行，并且会话将再次不可访问。

对于 **WaitForEvent** 调用的持续时间（尤其是在通知事件回调和处理筛选规则时），引擎处于称为 "等待内" 的状态。 在此状态下，不能 (调用 **WaitForEvent** ，因为它不是可重入) 。

在目标中启动执行涉及两个步骤：设置执行状态，然后调用 **WaitForEvent**。 可以使用方法 [**SetExecutionStatus**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setexecutionstatus) 或通过执行设置执行状态的调试器命令（例如， **g (中转)** 和 **p (步骤)**）来设置执行状态。

如果一系列调试器命令一起执行（例如 "**g;？@ $ip**"--如果该命令不是序列中的最后一个命令，则在目标中需要执行的任何命令后，将发生 *隐式等待* 。 如果调试器引擎处于 "等待内" 状态，则不会发生隐式等待;在这种情况下，将停止执行命令，并将当前命令（尝试导致隐式等待的命令）解释为目标中的执行如何继续。 其余的命令将被丢弃。

**注意**   在确定会话是否可访问或无法访问时， (的目标（例如，单步执行) 被视为由引擎执行。 当有限执行完成后，会话将可供访问。

 

### <a name="span-idhost_enginespanspan-idhost_enginespanhost-engine"></a><span id="host_engine"></span><span id="HOST_ENGINE"></span>主机引擎

远程调试时，可以使用调试器引擎的多个实例。 其中的一个实例正好维护调试会话;此实例称为 *主机引擎*。

所有调试器操作都与宿主引擎相关，例如，符号加载和扩展加载。

 

