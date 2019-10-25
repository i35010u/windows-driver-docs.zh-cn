---
title: 了解 TPS 组件
description: 了解 TPS 组件
ms.assetid: 4bc962fa-8c05-4b0f-b634-9c0f435907b7
keywords:
- 事务处理系统 WDK KTM，组件
- TPS WDK KTM，组件
- 事务处理系统 WDK KTM，方案
- TPS WDK KTM，方案
- TPS 的资源管理器 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b95cb452906859bedf6bee584e41a97e6de1a892
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836095"
---
# <a name="understanding-tps-components"></a>了解 TPS 组件


使用内核事务管理器（KTM）和[公用日志文件系统](using-common-log-file-system.md)（CLFS）的任何[*事务处理系统*](transaction-processing-terms.md#ktm-term-transaction-processing-system)（TPS）应包含以下重要组件：

-   [*事务管理器*](transaction-processing-terms.md#ktm-term-transaction-manager)（KTM）

    KTM 跟踪每个事务的状态，并在系统崩溃后协调恢复操作。

-   一个或多个[*资源管理器*](transaction-processing-terms.md#ktm-term-resource-manager)

    您提供的资源管理器可管理与每个事务关联的数据。

-   一个或多个 CLFS [*日志流*](transaction-processing-terms.md#ktm-term-log-stream)

    事务管理器和资源管理器使用 CLFS 日志流来记录可用于提交、回滚或恢复事务的信息。

-   一个或多个[*事务客户端*](transaction-processing-terms.md#ktm-term-transactional-client)

    通常，你的 TPS 的每个事务客户端都可以创建一个事务，对该事务的上下文中的数据执行操作，然后启动该事务的提交或回滚操作。

本主题向你介绍了一个[简单的 tps](#simple-tps) ，其中包含一个资源管理器、一个包含[多个资源](#multiple-resource-managers-in-a-tps)管理器的更复杂 TPS 以及一些[其他 tps 方案](#other-tps-scenarios)。

[使用 ktm](using-ktm.md)部分提供有关如何使用 KTM 创建 TPS 组件的详细信息。

### <a name="simple-tps"></a>简单 TPS

简单 TPS 可能由 KTM、一个资源管理器和 CLFS 组成。 事务性客户端可以通过资源管理器提供的接口与资源管理器进行通信。

例如，假设要创建数据库管理系统。 您希望您的系统的客户端可以通过打开数据库对象的句柄，对对象执行读写操作，然后关闭对象句柄来访问数据库。

现在，假设您想要以原子方式对读取和写入操作进行设置，以便系统的其他用户只能看到最终结果。 您可以通过设计一个 TPS，使客户端能够将一组数据库操作绑定到一个事务来实现该目标。

系统应包括一个资源管理器，该管理器管理数据库中的数据，以响应来自客户端的读取和写入请求。 此资源管理器可以导出一个应用程序编程接口（API），该接口使客户端能够将事务与一组读写操作相关联。

加载资源管理器时，它必须通过调用[**ZwCreateTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)和[**ZwCreateResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)向 KTM 注册自身。 然后，资源管理器可以参与事务。

你可能希望资源管理器支持一组函数，这些函数使客户端能够创建数据对象、读取和写入与数据对象相关联的数据，并关闭数据对象。 以下伪代码显示了来自客户端的代码序列示例。

```cpp
CreateDataObject (IN TransactionID, OUT DataHandle);
ReadData (IN DataHandle, OUT Data);
WriteData (IN DataHandle, IN Data);
WriteData (IN DataHandle, IN Data);
WriteData (IN DataHandle, IN Data);
CloseDataObject (IN DataHandle);
```

客户端在调用资源管理器的*CreateDataObject*例程之前，必须通过调用 KTM 的[**ZwCreateTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransaction)例程来创建事务对象，并通过调用[**ZwQueryInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransaction)。

当客户端调用资源管理器的*CreateDataObject*例程时，客户端会将该事务对象的标识符传递给资源管理器。 资源管理器可以调用[**ZwOpenTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransaction)来获取事务对象的句柄，然后它可以调用[**ZwCreateEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)来注册其参与事务。

此时，客户端可以开始对数据对象执行操作。 因为客户端在创建数据对象时提供了事务标识符，所以资源管理器可以将所有读取和写入操作分配给该事务。

资源管理器必须记录客户端指定的所有数据操作结果，而不会使结果成为永久结果。 通常情况下，资源管理器使用 CLFS 将操作结果记录到事务日志流中。

当客户端已经完成调用资源管理器以执行事务操作时，它将调用 KTM 的[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)例程。 此时，KTM[通知](transaction-notifications.md)资源管理器它应使操作永久运行。 然后，资源管理器会将操作结果从日志流移动到数据的永久性存储介质。 最后，资源管理器调用[**ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)来通知 KTM 提交操作已完成。

如果资源管理器报告某个客户端对*ReadData*或*WriteData*的调用之一出现错误，会发生什么情况？ 客户端可以调用[**ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction)来回滚事务。 此调用的结果是，KTM 通知资源管理器它应将数据还原到其原始状态。 然后，客户端可以为相同操作创建新事务，也可以选择不继续。

以下伪代码显示了客户端事务操作的更详细序列的示例。

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

如果在事务创建之后但在提交或回滚事务之前系统崩溃，会发生什么情况？ 每次加载资源管理器时，它都应调用[**ZwRecoverTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)和[**ZwRecoverResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)。 调用**ZwRecoverTransactionManager**会导致 KTM 打开其日志流并读取事务历史记录。 调用**ZwRecoverResourceManager**会导致 KTM 向资源管理器通知在发生崩溃之前正在进行的任何已登记事务，并通知资源管理器必须恢复哪些事务。

如果事务客户端在发生崩溃之前为事务调用了[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction) ，并开始处理事务的提交操作，则资源管理器必须能够将事务的状态还原到紧靠致使. 如果客户端未准备好在崩溃之前提交事务，则资源管理器可以丢弃数据并回滚事务。

有关如何编写事务客户端的详细信息，请参阅[创建事务客户端](creating-a-transactional-client.md)。

有关如何编写资源管理器的详细信息，请参阅[创建资源管理器](creating-a-resource-manager.md)。

### <a name="multiple-resource-managers-in-a-tps"></a>TPS 中的多个资源管理器

现在假设你的 TPS 使客户端能够在单个事务中修改两个不同数据库中的信息，以便仅当两个数据库的修改都成功时，事务才会成功。

在这种情况下，TPS 可以有两个资源管理器，每个数据库一个。 每个资源管理器都可以导出一个 API，客户端可以使用该 API 来访问资源管理器的数据库。

下面的伪代码演示了客户端如何创建单个事务，其中包含两个资源管理器支持的两个数据库上的操作。

在此示例中，客户端读取第一个数据库中的数据，并将其写入第二个数据库。 然后，客户端从第二个数据库中读取数据，并将其写入第一个数据库。 （第一个资源管理器导出函数以**Rm1**开头，第二个资源管理器导出以**Rm2**开头的函数。）

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

由于客户端将相同的事务标识符传递给两个资源管理器，因此两个资源管理器都可以调用[**ZwOpenTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransaction)和[**ZwCreateEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)以在事务中登记。 当客户端最终调用[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)时，KTM 会[通知](transaction-notifications.md)每个资源管理器，管理器应将操作设置为永久操作，并且每个资源管理器会在完成时调用[**ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete) 。

### <a name="other-tps-scenarios"></a>其他 TPS 方案

KTM 支持其他 TPS 方案。 例如，以下方案描述了 TPS 可能包含的组件：

-   管理多个数据库的一个资源管理器。

    资源管理器的 API 可以使客户端一次打开和访问多个数据库，并且客户端可以将对多个数据库的访问合并到一个事务中。

-   一个资源管理器，其中包含客户端调用的 API，以及包含第一个资源管理器调用的 Api 的其他资源管理器。

    客户端仅与第一个资源管理器通信。 当资源管理器处理来自客户端的请求时，它可以根据需要访问其他资源管理器来处理客户端的请求。 例如，资源管理器管理客户端可访问的数据库，该数据库需要从另一个资源管理器对客户端不可用的备份或数据验证操作。

-   不使用 KTM 的现有客户端和资源管理器与一组使用 KTM 的其他资源管理器集成。

    在这种情况下，您通常必须修改现有的资源管理器，使其成为与 KTM 通信的[上级事务管理](creating-a-superior-transaction-manager.md)器。

 

 




