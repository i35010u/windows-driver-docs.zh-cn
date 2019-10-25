---
title: 处理提交操作
description: 处理提交操作
ms.assetid: 4885476e-ce68-4674-b8a5-8a317f33cd5b
keywords:
- 事务 WDK KTM，提交事务
- 提交事务 WDK KTM
- 资源管理器 WDK KTM，提交事务
- 单阶段提交 WDK KTM，多阶段提交 WDK KTM
- 预先准备阶段 WDK KTM
- 准备阶段 WDK KTM
- 提交阶段 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b30cd5f4c33a13af27c5d6b511fd70ce37b1eed5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836590"
---
# <a name="handling-commit-operations"></a>处理提交操作


有两种类型的提交操作：*单阶段提交*和*多阶段提交*。 单阶段提交操作包含资源管理器必须响应的单个通知，而多阶段提交操作则包含用于准备步骤的其他通知。

单阶段提交操作更容易实现。 它适用于具有以下特征之一的事务处理系统（TPSs）：

-   单个资源管理器。

-   多个资源管理器，但其中一个资源管理器是[只读](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)的，不参与提交操作。

如果多个资源管理器参与提交操作，则需要执行多阶段提交操作。

### <a name="single-phase-commit-operations"></a>单阶段提交操作

如果你希望 TPS 支持单阶段提交操作，则一个（且仅有一个） resource manager 必须注册接收事务\_通知\_单\_阶段\_其登记的提交[通知](transaction-notifications.md)。 所有其他资源管理器都必须是[只读](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)的。

包含[上级事务管理器](creating-a-superior-transaction-manager.md)的 TPS 不能使用单阶段提交。

如果资源管理器已注册接收事务\_通知\_单\_阶段\_提交通知，则在事务客户端调用[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)时，KTM 发送此类通知。

当资源管理器收到事务\_通知\_单\_阶段\_提交事务的提交通知时，它可以提交事务或拒绝单阶段提交。

若要提交事务，资源管理器必须执行以下操作：

1.  刷新在非永久性缓存（内存中存储）中保留的任何数据，例如[CLFS 日志流](using-log-streams-with-ktm.md)的[CLFS 封送区](clfs-marshalling-areas.md)。

    资源管理器必须将数据从缓存移到持久存储介质。 例如，使用 CLFS 的资源管理器可以调用[**ClfsFlushBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsflushbuffers)。

2.  将所有数据更改设置为永久性和公共（即，在 resource manager 的范围之外可见）。

3.  调用[**ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)。

调用**ZwCommitComplete**后，资源管理器应调用[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)以关闭登记句柄。

若要拒绝事务的单阶段提交操作，资源管理器可以调用[**ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)。 如果资源管理器调用**ZwSinglePhaseReject**，则 KTM 会立即将提交操作从单阶段更改为多阶段。

如果其他资源管理器登记在同一事务中，则它们必须是[只读](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)的。 但是，它们必须注册以接收事务\_通知\_RM\_中断式通知，如果处理单阶段提交操作的资源管理器未指示它已提交或回滚事务。

### <a name="multi-phase-commit-operations"></a>多阶段提交操作

当发生以下事件之一时，将开始执行多阶段提交操作：

-   事务性客户端调用[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)，但没有资源管理器注册接收事务\_通知\_单\_阶段\_提交通知。

-   资源管理器在接收到事务后调用[**ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)\_通知\_单\_阶段\_提交通知。

-   [上级事务管理器](creating-a-superior-transaction-manager.md)调用[**ZwPrePrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)。

多阶段提交操作由三个连续阶段组成：*预准备*、*准备*和*提交*。

**准备阶段**

Commit 操作的预先准备阶段（也称为*阶段零*）将在 KTM 发送事务时开始\_通知所有资源管理器\_PREPREPARE 通知。 如果资源管理器不支持事务的单阶段提交操作，或者如果上级事务管理器调用[**ZwPrePrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)，则 KTM 将发送此通知。

当每个资源管理器收到事务\_通知\_PREPREPARE 通知时，它必须执行以下操作：

1.  刷新在非永久性缓存（内存中存储）中保留的任何数据，例如[CLFS 日志流](using-log-streams-with-ktm.md)的[CLFS 封送区](clfs-marshalling-areas.md)。

    资源管理器必须将数据从缓存移到持久存储介质。 例如，使用 CLFS 的资源管理器可以调用[**ClfsFlushBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsflushbuffers)。

2.  调用[**ZwPrePrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)。

资源管理器调用**ZwPreprepareComplete**后，可以继续接收和服务客户端请求。 但资源管理器必须将所有数据修改视为缓存传递操作，这些操作会立即写入持久存储介质。

如果资源管理器在处理事务时遇到错误\_通知\_PREPREPARE 通知，应调用[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)来回滚事务。

**准备阶段**

提交操作的准备阶段（也称为*第一阶段*）在 KTM 发送事务时开始，\_通知所有资源管理器\_准备通知。 如果任何资源管理器都不支持单阶段提交，或者上级事务管理器调用[**ZwPrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)，则 KTM 将在 TRANSACTION\_通知\_PREPREPARE。

当每个资源管理器收到事务\_通知\_准备通知时，必须执行以下操作：

1.  停止服务客户端请求，并将任何客户端后续请求报告为客户端错误。

2.  请确保所有数据都已移动到持久存储。

3.  调用[**ZwPrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)。

如果资源管理器在处理事务时遇到错误\_通知\_准备通知，应调用[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)来回滚事务。 但是，资源管理器在调用**ZwPrepareComplete**后将无法回滚事务。

**提交阶段**

提交操作的提交阶段（也称为第*二阶段*）在 KTM 发送事务时开始\_向所有资源管理器通知\_提交通知。 如果没有资源管理器支持单阶段提交，或者上级事务管理器调用[**ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)，则 KTM 在事务\_后发送此通知\_准备。

当每个资源管理器收到事务\_通知\_提交通知时，它必须执行以下操作：

1.  将所有数据更改设置为永久性和公共（即对其他事务可见）。

    通常情况下，资源管理器通过将事务的已保存数据从日志流复制到数据库的公共永久性存储，使更改成为永久更改。 有关如何使用日志流的详细信息，请参阅[使用 KTM 的日志流](using-log-streams-with-ktm.md)。

2.  调用[**ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)。

资源管理器调用**ZwCommitComplete**后，应调用[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)来关闭登记句柄。

如果资源管理器在处理事务时遇到错误\_通知\_提交通知，应自行关闭。 下次操作系统重新加载资源管理器时，资源管理器的[恢复过程](handling-recovery-operations.md)应将事务还原到在出现错误之前已知良好的状态。

 

 




