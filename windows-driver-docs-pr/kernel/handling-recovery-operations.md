---
title: 处理恢复操作
description: 处理恢复操作
ms.assetid: 35149bb9-fd48-44d3-a9fd-0e631aa0e853
keywords:
- 事务 WDK KTM，恢复事务
- 恢复事务 WDK KTM
- 事务处理系统 WDK KTM，恢复事务
- TPS WDK KTM，恢复事务
- 日志流 WDK KTM，恢复事务
- 虚拟时钟值 WDK KTM，恢复事务
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23583408bbf85be992ab57062ec5f23c0790e37c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190991"
---
# <a name="handling-recovery-operations"></a>处理恢复操作


在 *恢复* 操作中，事务处理系统 (TPS) 尝试从 [日志流](using-log-streams-with-ktm.md)中的信息恢复其状态。 恢复操作完成后，所有事务都应处于已提交或已回滚状态，并且所有资源数据应处于已知的良好状态。

有时，TPS 会在其所有事务完成之前停止。 例如，操作系统可能会崩溃。 因此，资源管理器必须在启动时启动恢复操作。 恢复操作将尝试确定是否有任何事务未完成。 如果在日志中找到了不完整的事务，则恢复操作将尝试提交或回滚这些事务。

对于基于 KTM 的 TPS，每个恢复操作都包含两个步骤。 第一步是从事务管理器对象的日志流中恢复信息。 第二步涉及到从资源管理器的日志流中恢复信息。

TPS 可以恢复到所有日志流的末尾，或者，如果其资源管理器维护 [虚拟时钟值](using-virtual-clock-values.md)，则它可以恢复到指定的时钟值。

### <a name="recovering-information-from-a-transaction-manager-objects-log-stream"></a>从事务管理器对象的日志流中恢复信息

资源管理器在调用 [**ZwCreateTransactionManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager) 或 [**ZwOpenTransactionManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransactionmanager)后立即调用 [**ZwRecoverTransactionManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)。 **ZwRecoverTransactionManager**例程读取属于事务管理器对象的日志流。 此例程会重新构造事务管理器对象的状态， (包括日志流中的恢复信息) 的所有事务、登记和资源管理器，从 KTM 在流的结尾处创建并结束的上一个 [重新开始区域](reading-restart-records-from-a-clfs-stream.md) 开始。

若要从上一次重新启动区域恢复到指定的虚拟时钟值，资源管理器可以调用 [**ZwRollforwardTransactionManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollforwardtransactionmanager) 而不是 **ZwRecoverTransactionManager**。

### <a name="recovering-information-from-a-resource-managers-log-stream"></a>从资源管理器的日志流中恢复信息

资源管理器在调用 [**ZwCreateResourceManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager) 或 [**ZwOpenResourceManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenresourcemanager)后立即调用 [**ZwRecoverResourceManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)。 **ZwRecoverResourceManager**例程尝试恢复与每个资源管理器的登记关联的事务。

当资源管理器调用 **ZwRecoverResourceManager**时，KTM 将 \_ \_ 为每个资源管理器的登记发送事务通知恢复 [通知](transaction-notifications.md) 。 资源管理器每次[**ZwRecoverEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment)收到其中一个事务 \_ 通知恢复通知时都必须调用 ZwRecoverEnlistment \_ 。

当资源管理器调用 **ZwRecoverEnlistment**时，KTM 将发送以下通知之一：

-   事务 \_ 通知 \_ 提交

    资源管理器必须使用其日志流中的信息来提交事务，然后必须调用 [**ZwCommitComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)。

-   事务 \_ 通知 \_ 回滚

    资源管理器必须使用其日志流中的信息来回滚事务，然后必须调用 [**ZwRollbackComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)。

-   事务 \_ 通知 \_ INDOUBT

    KTM 未确定事务的状态，稍后将发送 commit 或 rollback 通知。

通常，当 KTM 确定在 \_ \_ 该 TPS 停止并重新启动之前调用 [**ZwPrepareComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete) 的所有资源管理器时，它会发送事务通知提交通知。 \_ \_ 如果 KTM 确定一个或多个资源管理器未调用**ZwPrepareComplete**，则 KTM 将发送事务通知回滚通知。

当 KTM 发送 \_ \_ 每个登记的事务通知恢复通知后，它将发送事务 \_ 通知 \_ 上一次 \_ 恢复通知。

如果资源管理器调用 **ZwRollforwardTransactionManager** 而不是 **ZwRecoverTransactionManager**，则它必须仅恢复到它指定给 **ZwRollforwardTransactionManager**的虚拟时钟值。

资源管理器可以调用 [**ZwSetInformationEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationenlistment) 来设置自定义的恢复信息。 KTM 保存此信息并将其写入日志流，但 KTM 不尝试解释信息。 资源管理器可以通过调用 [**ZwQueryInformationEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationenlistment)随时检索恢复信息。

[高级事务管理器](creating-a-superior-transaction-manager.md) 有时在 \_ \_ 恢复操作期间接收事务通知恢复 \_ 查询通知。

 

