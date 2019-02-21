---
title: 了解 TP 组件
description: 了解 TP 组件
ms.assetid: 4bc962fa-8c05-4b0f-b634-9c0f435907b7
keywords:
- 事务处理系统 WDK KTM，组件
- TP WDK KTM 组件
- 事务处理系统 WDK KTM，方案
- TP WDK KTM 方案
- 资源管理器 WDK KTM，在 TP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66708e2418a48d30492986900b278f39781817db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524602"
---
# <a name="understanding-tps-components"></a>了解 TP 组件


任何[*事务处理系统*](transaction-processing-terms.md#ktm-term-transaction-processing-system) (TPS)，它使用内核事务管理器 (KTM) 和[公用日志文件系统](using-common-log-file-system.md)(CLFS) 应包含以下重要的组件：

-   一个[*事务管理器*](transaction-processing-terms.md#ktm-term-transaction-manager) (KTM)

    KTM 跟踪每个事务的状态，并在系统崩溃后恢复操作进行协调。

-   一个或多个[*资源管理器*](transaction-processing-terms.md#ktm-term-resource-manager)

    资源管理器，你提供管理与每个事务相关联的数据。

-   一个或多个 CLFS [*日志流*](transaction-processing-terms.md#ktm-term-log-stream)

    事务管理器和资源管理器使用 CLFS 日志流传输到可用于提交、 回滚或恢复事务的记录信息。

-   一个或多个[*事务客户端*](transaction-processing-terms.md#ktm-term-transactional-client)

    通常情况下，在 TP 每个事务客户端可以创建一个事务、 对数据执行操作的上下文中的事务，并启动的事务提交或回滚操作。

本主题为你介绍[简单 TP](#simple-tps)一个资源管理器中，使用更复杂的 TP 包含[多个资源管理器](#multiple-resource-managers-in-a-tps)，和一些[其他 TP 方案](#other-tps-scenarios)。

[使用 KTM](using-ktm.md)部分提供有关如何使用 KTM 创建 TP 组件的详细的信息。

### <a name="simple-tps"></a>Simple TPS

KTM、 一个资源管理器和 CLFS 可能包含简单 TPS。 事务的客户端可以与资源管理器通过资源管理器提供的接口通信。

例如，假设你想要创建的数据库管理系统。 希望您的系统的客户端通过执行读取和写入操作在对象上的打开的句柄的数据库对象，然后关闭对象句柄访问数据库。

现在假设您希望集的读取和写入操作的系统的其他用户查看仅对最终结果以原子方式发生。 可以通过设计使客户端能够绑定到事务的数据库操作组的 TP 实现该目标。

您的系统应包括资源管理器，用于管理数据库中读取和写入请求从客户端的响应中的数据。 此资源管理器无法导出应用程序编程接口 (API)，使客户端以将事务与读取的一组相关联操作和写操作。

加载资源管理器时，它必须注册其自身与 KTM 通过调用[ **ZwCreateTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566430)并[ **ZwCreateResourceManager**](https://msdn.microsoft.com/library/windows/hardware/ff566427). 然后，资源管理器可以参与事务。

您可能希望在资源管理器支持一组函数，使客户端来创建数据对象、 读取和写入与数据对象中，关联的数据并关闭数据对象。 下面的伪代码显示从客户端的示例代码序列。

```cpp
CreateDataObject (IN TransactionID, OUT DataHandle);
ReadData (IN DataHandle, OUT Data);
WriteData (IN DataHandle, IN Data);
WriteData (IN DataHandle, IN Data);
WriteData (IN DataHandle, IN Data);
CloseDataObject (IN DataHandle);
```

客户端可以调用所需的资源管理器的前*CreateDataObject*例程，客户端必须创建事务对象通过调用 KTM 的[ **ZwCreateTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff566429)例程，并通过调用获取事务对象的标识符[ **ZwQueryInformationTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff567057)。

当客户端调用所需的资源管理器的*CreateDataObject*例程，客户端传递的事务对象的标识符对资源管理器。 资源管理器可以调用[ **ZwOpenTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff567033)若要获取的句柄的事务对象，然后可以调用[ **ZwCreateEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff566422)注册其参与事务。

此时，客户端可以开始对数据对象执行操作。 由于客户端提供事务标识符，它创建的数据对象时，资源管理器可以将所有读取和写入操作都分配给该事务。

资源管理器必须记录数据操作，而无需进行结果永久指定客户端的所有的结果。 通常情况下，资源管理器使用 CLFS 中事务日志流记录的操作结果。

当客户端完成后调用资源管理器执行事务操作时，它将调用 KTM 的[ **ZwCommitTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff566420)例程。 此时，KTM[通知](transaction-notifications.md)，这可以使操作永久资源管理器。 资源管理器然后将操作结果从日志流到永久存储介质中的数据。 最后，资源管理器调用[ **ZwCommitComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff566418)通知 KTM 提交操作已完成。

如果资源管理器报告的客户端的调用的其中一个错误，会发生什么情况*ReadData*或*WriteData*？ 客户端可以调用[ **ZwRollbackTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff567086)回滚该事务。 进行该调用后，KTM 通知资源管理器，它应将数据还原到其原始状态。 然后，客户端可以创建新的事务进行相同的操作，或者可以选择以继续。

下面的伪代码显示了一系列更详细的客户端的事务性操作的示例。

```cpp
    ZwCreateTransaction (&TransactionHandle, ...);
    ZwQueryInformationTransaction (TransactionHandle, ...);
    CreateDataObject (TransactionID, &DataHandle);
    Status = ReadData (DataHandle, &Data1);
    if (Status == Error) goto ErrorRollback;
    Status = WriteData (DataHandle, Data2);
    if (Status == Error) goto ErrorRollback;
    Status = WriteData (DataHandle, Data3);
    if (Status == Error) goto ErrorRollback;
    Status = WriteData (DataHandle, Data4);
    if (Status == Error) goto ErrorRollback;
    ZwCommitTransaction (TransactionHandle, ...);
    goto Leave;
ErrorRollback:
    ZwRollbackTransaction (TransactionHandle, ...);
Leave:
    ZwClose (TransactionHandle);
    return;
```

如果在系统崩溃后的事务创建，但在提交或回滚之前，会发生什么情况？ 应调用资源管理器加载，每次[ **ZwRecoverTransactionManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567079)并[ **ZwRecoverResourceManager** ](https://msdn.microsoft.com/library/windows/hardware/ff567078). 调用**ZwRecoverTransactionManager**导致 KTM 打开其日志流并读取的事务历史记录。 调用**ZwRecoverResourceManager**导致 KTM 通知任何已登记事务都在崩溃前的正在进行中的资源管理器和哪些事务资源管理器因此必须恢复。

如果事务的客户端调用[ **ZwCommitTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff566420)对于在崩溃前的事务并开始处理事务的提交操作，必须能够还原资源管理器事务的状态设置为之前在发生崩溃的点。 如果客户端未准备好提交事务在崩溃前的，资源管理器可以丢弃数据，并回滚事务。

有关如何编写事务性客户端的详细信息，请参阅[创建事务的客户端](creating-a-transactional-client.md)。

有关如何编写资源管理器的详细信息，请参阅[资源管理器创建](creating-a-resource-manager.md)。

### <a name="multiple-resource-managers-in-a-tps"></a>在 TP 中的多个资源管理器

现在假设您 TP 使客户端能够修改在单个事务中的两个单独数据库中的信息，以便仅当这两个数据库的修改成功，事务获得成功。

在这种情况下，在 TP 可以有两个资源管理器，一个用于每个数据库。 每个资源管理器可以导出一个 API，客户端可用来访问资源管理器的数据库。

下面的伪代码展示了客户端如何创建包含两个资源管理器支持的两个数据库上的操作的单个事务。

在此示例中，客户端从第一个数据库中读取数据并将其写入到第二个数据库。 然后，客户端从第二个数据库中读取数据并将其写入的第一个数据库。 (第一个资源管理器导出函数的开头**Rm1**，并第二个资源管理器将导出函数的开头**Rm2**。)

```cpp
    ZwCreateTransaction (&TransactionHandle, ...);
    ZwQueryInformationTransaction (TransactionHandle, ...);
    Rm1CreateDataObject (TransactionID, &Rm1DataHandle);
    Rm2CreateDataObject (TransactionID, &Rm2DataHandle);
    Status = Rm1ReadData (Rm1DataHandle, &Rm1Data);
    if (Status == Error) goto ErrorRollback;
    Status = Rm2WriteData (Rm2DataHandle, Rm1Data);
    if (Status == Error) goto ErrorRollback;
    Status = Rm2ReadData (Rm2DataHandle, &Rm2Data);
    if (Status == Error) goto ErrorRollback;
    Status = Rm1WriteData (Rm1DataHandle, Rm2Data);
    if (Status == Error) goto ErrorRollback;
    ZwCommitTransaction (TransactionHandle, ...);
    goto Leave;
ErrorRollback:
    ZwRollbackTransaction (TransactionHandle, ...);
Leave:
    ZwClose (TransactionHandle);
    return;
```

由于客户端将相同的事务标识符传递给这两个资源管理器，可以调用这两个资源管理器[ **ZwOpenTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff567033)并[ **ZwCreateEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff566422)在事务中登记。 当客户端最终调用[ **ZwCommitTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff566420)，KTM[通知](transaction-notifications.md)管理器应该建立操作永久的并且每个每个资源管理器资源管理器调用[ **ZwCommitComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff566418)是否已完成。

### <a name="other-tps-scenarios"></a>其他 TP 方案

KTM 支持其他 TP 方案。 例如，下面的方案描述 TP 可能包含的组件：

-   管理多个数据库的一个资源管理器。

    资源管理器 API 可以使客户端能够打开并一次访问多个数据库和客户端可以合并到单个事务中的多个数据库的访问。

-   一个资源管理器 api 的客户端调用，并与第一个资源管理器调用的 Api 的附加资源管理器。

    客户端仅与第一个资源管理器进行通信。 当该资源管理器处理客户端的请求时，它可以访问其他资源管理器，根据需要来处理客户端的请求。 例如，资源管理器管理的客户端访问数据库，需要从不供客户端的第二个资源管理器的备份或数据验证操作。

-   现有的客户端和资源管理器不使用 KTM，与一组额外的资源管理器使用 KTM 的集成。

    在这种情况下，通常需要修改现有的资源管理器，以使其成为[上级事务管理器](creating-a-superior-transaction-manager.md)与 KTM 的通信。

 

 




