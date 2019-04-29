---
title: 处理恢复操作
description: 处理恢复操作
ms.assetid: 35149bb9-fd48-44d3-a9fd-0e631aa0e853
keywords:
- WDK KTM，恢复事务的事务
- 恢复 WDK KTM 的事务
- 事务处理系统 WDK KTM、 恢复事务
- TP WDK KTM，恢复事务
- 日志流 WDK KTM，恢复事务
- 虚拟时钟值 WDK KTM，恢复事务
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b361b60f451f98f42b58be5544265015abf5bb11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384652"
---
# <a name="handling-recovery-operations"></a>处理恢复操作


在中*恢复*操作，事务处理系统 (TPS) 会尝试恢复其状态中的信息[日志流](using-log-streams-with-ktm.md)。 恢复操作完成后，所有事务应在提交或回滚返回状态，并且资源的所有数据都应在已知的良好状态。

有时 TP 停止之前完成其所有事务。 例如，操作系统可能会崩溃。 因此，资源管理器必须启动恢复操作时开始运行。 恢复操作会尝试确定任何事务都不完整。 如果未完成的事务日志中找到，恢复操作将尝试提交或回滚这些事务。

对于基于 KTM 的 TP，每个恢复操作由两个步骤组成。 第一步涉及从事务管理器对象的日志流恢复信息。 第二个步骤包括从资源管理器的日志流恢复信息。

TP 可以恢复到的所有日志流的结尾或其资源管理器维护[虚拟时钟值](using-virtual-clock-values.md)，它可以恢复到指定的时钟值。

### <a name="recovering-information-from-a-transaction-manager-objects-log-stream"></a>从事务管理器对象的日志 Stream 恢复信息

资源管理器立即调用后[ **ZwCreateTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566430)或[ **ZwOpenTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff567035)，必须调用[ **ZwRecoverTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff567079)。 **ZwRecoverTransactionManager**例程读取日志流所属的事务管理器对象。 此例程是在日志流中，从最后一个处开始的恢复信息从重新构造 （包括所有事务，登记和资源管理器） 的事务管理器对象的状态[重新开始区域](reading-restart-records-from-a-clfs-stream.md)该 KTM 创建而结束于流的末尾。

若要恢复从最后一个直到达到指定的虚拟时钟值重新开始区域，资源管理器可以调用[ **ZwRollforwardTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567089)而不是**ZwRecoverTransactionManager**.

### <a name="recovering-information-from-a-resource-managers-log-stream"></a>从资源管理器的日志 Stream 恢复信息

资源管理器立即调用后[ **ZwCreateResourceManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566427)或[ **ZwOpenResourceManager**](https://msdn.microsoft.com/library/windows/hardware/ff567026)，它必须调用[**ZwRecoverResourceManager**](https://msdn.microsoft.com/library/windows/hardware/ff567078)。 **ZwRecoverResourceManager**例程尝试恢复的事务的关联与每个资源管理器的登记。

当资源管理器调用**ZwRecoverResourceManager**，KTM 发送事务\_通知\_恢复[通知](transaction-notifications.md)为每个资源管理器的登记。 资源管理器必须调用[ **ZwRecoverEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff567075)每次它接收一个事务\_通知\_恢复通知。

当资源管理器调用**ZwRecoverEnlistment**，KTM 发送一个以下通知：

-   事务\_通知\_提交

    资源管理器必须使用其日志的流中的信息以提交事务，然后必须调用[ **ZwCommitComplete**](https://msdn.microsoft.com/library/windows/hardware/ff566418)。

-   事务\_通知\_回滚

    资源管理器必须使用其日志的流中的信息以回滚事务，然后必须调用[ **ZwRollbackComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567081)。

-   事务\_通知\_INDOUBT

    KTM 尚未确定事务的状态，并将发送提交或回滚通知更高版本。

通常情况下，KTM 发送事务\_通知\_如果确定所有资源管理器都调用提交通知[ **ZwPrepareComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff567037) TPS 停止之前和重新启动。 KTM 发送事务\_通知\_回滚通知如果确定一个或多个资源管理器未调用**ZwPrepareComplete**。

KTM 已发送事务后\_通知\_每个登记的恢复通知，它将发送事务\_通知\_最后一个\_恢复通知。

如果资源管理器调用了**ZwRollforwardTransactionManager**而不是**ZwRecoverTransactionManager**，它必须最多的虚拟时钟值只恢复其指定给**ZwRollforwardTransactionManager**。

资源管理器可以调用[ **ZwSetInformationEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff567094)设置自定义的恢复信息。 KTM 保存此信息，并将其写入到日志流，但 KTM 不会尝试解释的信息。 资源管理器可以通过调用检索在任何时间的恢复信息[ **ZwQueryInformationEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567051)。

[高级事务管理器](creating-a-superior-transaction-manager.md)有时接收事务\_通知\_恢复\_恢复操作期间的查询通知。

 

 




