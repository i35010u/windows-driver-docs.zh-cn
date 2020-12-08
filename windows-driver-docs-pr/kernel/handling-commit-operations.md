---
title: 处理提交操作
description: 处理提交操作
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
ms.openlocfilehash: 75586d327f3202608c0e989665a22e97f9f75697
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785123"
---
# <a name="handling-commit-operations"></a>处理提交操作


有两种类型的提交操作： *单阶段提交* 和 *多阶段提交*。 单阶段提交操作包含资源管理器必须响应的单个通知，而多阶段提交操作则包含用于准备步骤的其他通知。

单阶段提交操作更容易实现。 它适用于具有以下特征之一 (TPSs) 的事务处理系统：

-   单个资源管理器。

-   多个资源管理器，但其中一个资源管理器是 [只读](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment) 的，不参与提交操作。

如果多个资源管理器参与提交操作，则需要执行多阶段提交操作。

### <a name="single-phase-commit-operations"></a>Single-Phase 提交操作

如果你希望 TPS 支持单阶段提交操作，一个 (并且只有一个) 资源管理器必须注册，以接收 \_ \_ \_ \_ 针对其登记的单阶段提交 [通知](transaction-notifications.md) 。 所有其他资源管理器都必须是 [只读](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)的。

包含 [上级事务管理器](creating-a-superior-transaction-manager.md) 的 TPS 不能使用单阶段提交。

如果资源管理器已注册接收事务 \_ 通知 \_ 单 \_ 阶段 \_ 提交通知，则在事务客户端调用 [**ZwCommitTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)时，KTM 将发送此类通知。

当资源管理器接收到事务 \_ 的 \_ 单 \_ 阶段 \_ 提交通知时，它可以提交事务或拒绝单阶段提交。

若要提交事务，资源管理器必须执行以下操作：

1.   (内存中存储) （如[CLFS 日志流](using-log-streams-with-ktm.md)的[CLFS 封送处理区](clfs-marshalling-areas.md)），刷新它在非永久性缓存中保存的所有数据。

    资源管理器必须将数据从缓存移到持久存储介质。 例如，使用 CLFS 的资源管理器可以调用 [**ClfsFlushBuffers**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsflushbuffers)。

2.  将所有数据更改设置为永久性的公共 (，即在 resource manager 范围外可见) 。

3.  调用 [**ZwCommitComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)。

调用 **ZwCommitComplete** 后，资源管理器应调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) 以关闭登记句柄。

若要拒绝事务的单阶段提交操作，资源管理器可以调用 [**ZwSinglePhaseReject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)。 如果资源管理器调用 **ZwSinglePhaseReject**，则 KTM 会立即将提交操作从单阶段更改为多阶段。

如果其他资源管理器登记在同一事务中，则它们必须是 [只读](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)的。 但是，它们必须注册以接收事务 \_ 通知 \_ RM \_ 断开连接通知，如果处理单阶段提交操作的资源管理器关闭了登记句柄，而没有指示它已提交或回滚事务，则会收到该通知。

### <a name="multi-phase-commit-operations"></a>多阶段提交操作

当发生以下事件之一时，将开始执行多阶段提交操作：

-   事务客户端调用 [**ZwCommitTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)，但没有资源管理器注册接收事务 \_ 通知 \_ 单 \_ 阶段 \_ 提交通知。

-   资源管理器在 [**ZwSinglePhaseReject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)收到事务 \_ 通知 \_ 单 \_ 阶段 \_ 提交通知后调用 ZwSinglePhaseReject。

-   [上级事务管理器](creating-a-superior-transaction-manager.md)调用 [**ZwPrePrepareEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)。

多阶段提交操作由三个连续阶段组成： *预准备*、 *准备* 和 *提交*。

**准备阶段**

当 KTM 向所有资源管理器发送事务通知 PREPREPARE 通知时，预准备阶段 (也称为 *阶段零*) 提交操作开始 \_ \_ 。 如果资源管理器不支持事务的单阶段提交操作，或者如果上级事务管理器调用 [**ZwPrePrepareEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)，则 KTM 将发送此通知。

当每个资源管理器收到事务 \_ 通知 \_ PREPREPARE 通知时，它必须执行以下操作：

1.   (内存中存储) （如[CLFS 日志流](using-log-streams-with-ktm.md)的[CLFS 封送处理区](clfs-marshalling-areas.md)），刷新它在非永久性缓存中保存的所有数据。

    资源管理器必须将数据从缓存移到持久存储介质。 例如，使用 CLFS 的资源管理器可以调用 [**ClfsFlushBuffers**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsflushbuffers)。

2.  调用 [**ZwPrePrepareComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)。

资源管理器调用 **ZwPreprepareComplete** 后，可以继续接收和服务客户端请求。 但资源管理器必须将所有数据修改视为缓存传递操作，这些操作会立即写入持久存储介质。

如果资源管理器在处理事务通知 PREPREPARE 通知时遇到错误 \_ \_ ，应调用 [**ZwRollbackEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment) 来回滚事务。

**准备阶段**

当 KTM 向所有资源管理器发送事务通知准备通知时，"准备" 阶段 (也称为 *阶段一*) 提交操作 \_ \_ 。 \_ \_ 如果没有资源管理器支持单阶段提交，或者上级事务管理器调用 [**ZWPREPAREENLISTMENT**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)，则 KTM 会在事务通知 PREPREPARE 后发送此通知。

当每个资源管理器收到事务 \_ 通知 \_ 准备通知时，它必须执行以下操作：

1.  停止服务客户端请求，并将任何客户端后续请求报告为客户端错误。

2.  请确保所有数据都已移动到持久存储。

3.  调用 [**ZwPrepareComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)。

如果资源管理器在处理事务通知准备通知时遇到错误 \_ \_ ，应调用 [**ZwRollbackEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment) 回滚事务。 但是，资源管理器在调用 **ZwPrepareComplete** 后将无法回滚事务。

**提交阶段**

当 KTM 向所有资源管理器发送事务通知提交通知时，提交操作的提交阶段 (也称为 *阶段 2*) \_ \_ 。 \_ \_ 如果没有资源管理器支持单阶段提交，或者上级事务管理器调用 [**ZWCOMMITENLISTMENT**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)，则 KTM 在事务通知准备后发送此通知。

当每个资源管理器收到事务 \_ 通知 \_ 提交通知时，它必须执行以下操作：

1.  将所有数据更改设置为永久性的公共 (，并对其他事务) 可见。

    通常情况下，资源管理器通过将事务的已保存数据从日志流复制到数据库的公共永久性存储，使更改成为永久更改。 有关如何使用日志流的详细信息，请参阅 [使用 KTM 的日志流](using-log-streams-with-ktm.md)。

2.  调用 [**ZwCommitComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)。

资源管理器调用 **ZwCommitComplete** 后，应调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) 来关闭登记句柄。

如果资源管理器在处理事务通知提交通知时遇到错误 \_ \_ ，则会自行关闭。 下次操作系统重新加载资源管理器时，资源管理器的 [恢复过程](handling-recovery-operations.md) 应将事务还原到在出现错误之前已知良好的状态。

 

