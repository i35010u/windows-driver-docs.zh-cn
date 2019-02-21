---
title: 调试会话和执行模型
description: 调试会话和执行模型
ms.assetid: 1cc2c055-447c-44cd-94d4-ae3dfa8243fb
keywords:
- 调试器引擎执行模型
- 执行模型
- 调试器引擎，在调试会话
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09572ce201eafbd0992ae04b22ea4071006b4bd2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543477"
---
# <a name="debugging-session-and-execution-model"></a>调试会话和执行模型


调试器引擎可以同时调试多个目标。 一个*调试会话*时开始，该引擎获取目标并将继续，直到已放弃的所有目标。 调试会话处于*无法访问*执行目标时，*可访问*挂起当前目标时。 引擎仅可用于检查和操作的目标，在会话处于可访问时。

调试程序的主循环通常包括设置调用方法的执行状态[ **WaitForEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff561229)和处理生成[事件](events.md#events)。 当**WaitForEvent**是调用，该会话将无法访问。

目标事件时，该引擎将挂起所有目标和会话将成为可访问。 然后，引擎通知事件的事件的回调，并遵循事件筛选器规则。 事件的回调和事件筛选器确定如何应继续执行在目标中。 如果他们确定引擎应进入调试器， **WaitForEvent**方法返回，并且会话仍可访问; 否则，引擎将继续执行的目标值以确定事件的方式回调和事件筛选器和会话将恢复无法访问。

持续时间**WaitForEvent**调用-具体而言，同时通知事件的回调并处理筛选器规则-引擎处于引用如"在等待"状态。 在此状态下， **WaitForEvent**不能调用 （它不是可重入）。

有两个步骤中启动目标中的执行涉及： 设置执行状态，然后再调用**WaitForEvent**。 可以使用方法设置的执行状态[ **SetExecutionStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff556693)或通过执行设置的执行状态-例如，一个调试器命令**g(Go)** 和**p （步骤）**。

如果调试器一系列的命令将执行--例如，"**g;？@$ ip**"-*隐式等待*如果该命令不是序列中的最后一个命令，则需要在目标中的执行任何命令后会发生。 调试器引擎状态是"内部等待"; 时，不会发生隐式等待在这种情况下，将停止执行的命令和当前命令-的尝试会导致隐式等待-将被解释为相对值的指示执行在目标中的应如何继续。 将丢弃其余的命令。

**请注意**  确定是否可访问该会话时或无法访问、 限制执行目标 （例如，单步执行） 被视为由引擎执行。 限制的执行完成后，会话将成为可访问。

 

### <a name="span-idhostenginespanspan-idhostenginespanhost-engine"></a><span id="host_engine"></span><span id="HOST_ENGINE"></span>主机引擎

当远程调试，可以使用调试器引擎的多个实例。 这些实例的一个维护调试会话;此实例称为*主机引擎*。

调试器的所有操作都都相对于主机引擎，例如，符号加载，加载的扩展。

 

 





