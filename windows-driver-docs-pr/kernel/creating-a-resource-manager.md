---
title: 创建资源管理器
description: 创建资源管理器
ms.assetid: b2841d56-650a-487c-a002-2521cd1b461b
keywords:
- 资源管理器 WDK KTM，创建资源管理器
- 登记 WDK KTM，只读登记
- 只读登记 WDK KTM
- 资源管理器 WDK KTM，易失性资源管理器
- 易失性资源管理器 WDK KTM
- 资源管理器 WDK KTM，将添加到 TP
- 事务处理系统 WDK KTM，添加资源管理器
- TP WDK KTM，添加资源管理器
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06706db926cbc3d7c062f0fabbc8042b1ef1ebe2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522312"
---
# <a name="creating-a-resource-manager"></a>创建资源管理器


[*资源管理器*](transaction-processing-terms.md#ktm-term-resource-manager)维护每个事务的数据和日志事务的操作。 如果事务处理系统 (TPS) 具有多个资源管理器，每个资源管理器可以参与每个事务的提交、 回滚和恢复操作。

每个资源管理器必须导出事务客户端可用来访问数据库或其他资源的资源管理器维护的接口。

通常情况下，内核模式资源管理器必须按列出顺序执行以下任务：

1.  创建日志流。

    可以使用资源管理器[公用日志文件系统](using-common-log-file-system.md)(CLFS)，或某些其他日志记录功能，以维护其日志流。 调用[ **ClfsCreateLogFile** ](https://msdn.microsoft.com/library/windows/hardware/ff540792)创建 CLFS 日志流。 资源管理器必须使用日志流记录提交、 回滚，或者事务进行恢复所需的任何信息。 此外，KTM 使用日志流记录可能需要恢复的事务的任何内部状态更改。

2.  创建一个事务管理器对象。

    调用[ **ZwCreateTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566430)创建的事务管理器对象并将资源管理器连接到资源管理器指定的其他 CLFS 日志流。

3.  恢复事务管理器状态。

    调用[ **ZwRecoverTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567079)读取对象的日志流 （这会保存 KTM） 事务管理器，并确定是否 TP 已关闭之前的所有事务都已完成的 （例如，因为系统已崩溃）。 KTM 还原日志流中的信息基于其内部状态。

4.  创建资源管理器对象。

    调用[ **ZwCreateResourceManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566427)创建资源管理器对象，并将其与先前创建的事务管理器对象关联。

5.  恢复资源管理器状态。

    调用[ **ZwRecoverResourceManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567078) KTM 发送事务的资源管理器将导致\_通知\_恢复通知的任何事务的正在进行中资源管理器关闭最后一个时间。 有关资源管理器应如何响应这些通知的信息，请参阅[处理恢复操作](handling-recovery-operations.md)。

6.  从客户端接收的事务。

    通常情况下，客户端创建事务对象，并使用资源管理器的客户端界面将传递给资源管理器的事务对象的 GUID。 例如，可能会提供资源管理器*CreateDataObject*类似于一个例程，[了解 TP 组件](understanding-tps-components.md)主题介绍。

7.  在每个事务中登记。

    调用[ **ZwOpenTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff567033)打开的句柄的事务对象，然后调用[ **ZwCreateEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff566422)创建事务的的登记。 登记，资源管理器，以接收一组指定的[事务通知](transaction-notifications.md)。

8.  启用接收事务通知。

    资源管理器可以调用[ **ZwGetNotificationResourceManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566467)以获取通知以同步方式，也可以调用[ **TmEnableCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff564676)注册*ResourceManagerNotification* KTM 调用通知可用时的回调例程。

9.  服务资源的访问请求来自客户端，但不能进行所做的更改永久。

    客户端创建事务对象后，它通常会调用资源管理器的界面来访问资源管理器的资源。 例如，数据库的资源管理器可能会收到请求，以读取和写入到数据库。

    资源管理器必须记录结果读取和写入操作[CLFS 日志流](using-log-streams-with-ktm.md)或其他日志记录功能，直到收到一条通知，该事务的操作将提交，回滚，或恢复。

10. 提交或回滚客户端操作。

    最终，资源管理器时接收通知以开始提交或回滚客户端已执行的操作。 在响应中，资源管理器必须使客户端操作永久或放弃它们。 有关如何处理提交和回滚通知的详细信息，请参阅[处理事务操作](handling-transaction-operations.md)。

    有时，可能需要尝试强制 KTM 快速提供提交或回滚的通知，可能是，因为资源管理器已确定设备被意外删除的资源管理器。 在这种情况下，可以调用资源管理器[ **TmRequestOutcomeEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff564727)。

11. 关闭登记对象句柄。

    资源管理器已完成处理该事务后，它必须调用[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)关闭登记对象的句柄

12. 关闭资源管理器对象句柄和事务管理器对象句柄。

    资源管理器卸载之前，必须调用[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)关闭资源管理器对象的句柄和事务管理器对象的句柄。

必须在资源管理器的初始化代码中执行步骤 1 至 5。 例如，如果资源管理器是一个内核模式驱动程序，初始化代码是在驱动程序[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程。

在响应请求事务的客户端的代码中通常执行步骤 6 到 11。

必须在资源管理器的最终清理代码，如内核模式驱动程序中执行步骤 12 [ *Unload* ](https://msdn.microsoft.com/library/windows/hardware/ff564886)例程。

## <a href="" id="kernel-creating-a-read-only-enlistment"></a> 创建只读登记


一个*只读登记*是未收到任何通知 KTM 的登记。 资源管理器可以将任何登记只读通过调用[ **ZwReadOnlyEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567074)。 此调用会导致 KTM 停止将通知传递到资源管理器。

后所需的资源管理器调用了具有[ **ZwCreateEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff566422)，它可以调用**ZwReadOnlyEnlistment**上随时从该处它可正常调用为止[**ZwPrepareComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567037)。

有两个原因可能想要调用在资源管理器的原因**ZwReadOnlyEnlistment**。

-   资源管理器具有已加入在事务中，并在某个时间点之前接收事务\_通知\_提交通知资源管理器确定它不再具有要参与该事务提交操作。

    例如，当资源管理器收到事务时，才\_通知\_准备通知时，它可能会确定所有事务的操作已更改资源管理器的数据库。 资源管理器可以调用**ZwReadOnlyEnlistment**而不是**ZwPrepareComplete**从事务中删除其自身。

-   资源管理器永远不会参与任何事务的提交操作。

    例如，资源管理器可以监视客户端发送，而无需修改任何存储的数据库的数据。 在这种情况下，可能会调用资源管理器**ZwReadOnlyEnlistment**立即该维度被称为后**ZwCreateEnlistment**。 此外，可以选择以使此类资源管理器*易失性*，如本主题的下一节中所述。

后一个资源管理器调用了具有**ZwReadOnlyEnlistment**，它可以调用[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)关闭登记句柄。

## <a href="" id="kernel-creating-a-volatile-resource-manager"></a> 创建易失性资源管理器


一个*易失性资源管理器*不维护持久数据作为资源管理器。 例如，可以创建易失性资源管理器监视数据的客户端发送，如果资源管理器不会修改持久存储的数据库。 易失性资源管理器通常不记录事务活动，因此无法执行恢复或回滚操作。

易失性资源管理器必须设置的资源\_管理器\_易失性标志时，它调用[ **ZwCreateResourceManager**](https://msdn.microsoft.com/library/windows/hardware/ff566427)。 如果设置此标志，则 KTM 不关联的事务管理器对象在日志流记录有关资源管理器的任何信息。

资源管理器还可以设置事务\_管理器\_易失性标志时，它调用[ **ZwCreateTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff566430)。 如果设置此标志，KTM 不创建的事务管理器对象的日志流。 此外，任何连接到事务管理器对象的附加资源管理器必须也是可变字段并将该资源\_MANAGER\_易失性标志。

## <a name="adding-a-resource-manager-to-an-existing-tps"></a>将资源管理器添加到现有的 TP


如果您必须将一个附加的资源管理器添加到现有的 TP，有两个选择：

-   新的资源管理器调用[ **ZwCreateTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566430)创建其自己的事务管理器对象。

    如果资源管理器不与其他资源管理器在 TP 中通信，请使用此选项。

-   新的资源管理器调用[ **ZwOpenTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567035)连接到现有的事务管理器对象。

    如果资源管理器必须与在 TP 中其他资源管理器进行通信，请使用此选项。 调用资源管理器**ZwCreateTransactionManager**必须共享该事务管理器对象的 GUID、 日志流名称或对象名称，以便其他资源管理器可以调用**ZwOpenTransactionManager**. 这些其他资源管理器可以调用[ **ZwQueryInformationTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567058)要获得有关的事务管理器对象的其他信息。

资源管理器添加到 TPS 后，了解资源管理器的客户端可以调用资源管理器的客户端接口。

 

 




