---
title: 事务通知
description: 事务通知
ms.assetid: 62169b56-e70f-4d32-a051-a7fd947dbc64
keywords:
- 通知 WDK KTM
- 事务 WDK KTM，通知
- 资源管理器 WDK KTM，通知
- 内核事务管理器 WDK 通知
- KTM WDK 通知
- 高级事务管理器 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d231f88e1dfca5914c354251e739799adc184be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382954"
---
# <a name="transaction-notifications"></a>事务通知


KTM 为每个资源管理器提供了通知队列。 KTM 将通知传递到资源管理器，通过将它们放在资源管理器的队列。

资源管理器可以在同步或异步方式从其队列检索通知。

-   若要以同步方式检索通知，资源管理器可以重复调用[ **ZwGetNotificationResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntgetnotificationresourcemanager)。

-   若要以异步方式接收通知，资源管理器可以调用[ **TmEnableCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmenablecallbacks)设置回调例程。 每次它会将通知放在资源管理器的队列时，KTM 调用回调例程。

当资源管理器调用[ **ZwCreateEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreateenlistment)若要创建一个事务的登记，资源管理器指定它应接收通知的类型。 资源管理器收到他们注册以接收的通知。

通知常量 Ktmtypes.h 中定义。 通知常量名具有事务的格式\_通知\_*Xxx*。

本主题的其余部分列出了所有通知常量 Ktmtypes.h 定义，并将它们划分为三个组：

-   资源管理器可以接收的通知

-   高级事务管理器可以接收的通知

-   已定义，但当前未使用的通知常量

### <a href="" id="notifications-for-resource-managers"></a> 通知资源管理器

所有资源管理器必须都注册才能接收事务\_通知\_PREPREPARE、 事务\_通知\_准备、 和事务\_通知\_提交通知，甚至如果它们随后调用[ **ZwReadOnlyEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntreadonlyenlistment)将标记为只读的登记。

资源管理器可以支持事务\_通知\_单个\_阶段\_提交，但它们必须还支持多阶段 pre-prepare、 准备和提交通知。

以下列表包含资源管理器可以接收的所有通知：

<a href="" id="transaction-notify-preprepare"></a>事务\_通知\_PREPREPARE  
**发送时**:在客户端调用[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction) ，并在没有资源管理器支持单阶段提交，或者，如果[上级事务管理器](creating-a-superior-transaction-manager.md)调用[ **ZwPrePrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreprepareenlistment)。

**收到的**:资源管理器。

**接收方所需的操作**:执行预先准备操作，然后调用[ **ZwPrePrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepreparecomplete)。 (有关详细信息预先准备操作，请参阅[处理提交操作](handling-commit-operations.md)。)

**以下限制：** 资源管理器还必须支持事务\_通知\_准备和事务\_通知\_提交。

<a href="" id="transaction-notify-prepare"></a>事务\_通知\_准备  
**发送时**:事务处理后\_通知\_PREPREPARE 如果客户端调用[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)并没有资源管理器支持单阶段提交，或如果高级事务管理器调用[ **ZwPrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepareenlistment)。

**收到的**:资源管理器。

**接收方所需的操作：** 执行准备操作，然后调用[ **ZwPrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreparecomplete)。 (有关详细信息准备操作，请参阅[处理提交操作](handling-commit-operations.md)。)

**以下限制：** 资源管理器还必须支持事务\_通知\_PREPREPARE 和事务\_通知\_提交。

<a href="" id="transaction-notify-commit"></a>事务\_通知\_提交  
**发送时**:事务处理后\_通知\_准备如果客户端调用[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)并没有资源管理器支持单阶段提交，或如果高级事务管理器调用[ **ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)。

**收到的**:资源管理器。

**接收方所需的操作**:执行提交操作，然后调用[ **ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitcomplete)。 (有关提交操作的详细信息，请参阅[处理提交操作](handling-commit-operations.md)。)

**以下限制：** 资源管理器还必须支持事务\_通知\_PREPREPARE 和事务\_通知\_准备。

<a href="" id="transaction-notify-single-phase-commit"></a>事务\_通知\_单个\_阶段\_提交  
**发送时**:在客户端调用[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)和资源管理器支持单阶段提交操作。

**收到的**:资源管理器。

**接收方所需的操作**:可以提交的事务或调用[ **ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsinglephasereject)。 (有关使用单阶段提交操作的详细信息，请参阅[处理提交操作](handling-commit-operations.md)。)

**以下限制：** 资源管理器还必须支持事务\_通知\_PREPREPARE、 事务\_通知\_准备、 和事务\_通知\_提交。

<a href="" id="transaction-notify-rollback"></a>事务\_通知\_回滚  
**发送时**:在客户端调用[ **ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbacktransaction)，上级事务管理器调用[ **ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackenlistment)，或者检测到 KTM错误 （如日志流失败的写入）。

**收到的**:资源管理器和高级事务管理器。

**接收方所需的操作**:执行任何操作来回滚该事务的数据，然后调用所需[ **ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackcomplete)。 (有关回滚操作的详细信息，请参阅[处理回滚操作](handling-rollback-operations.md)。)

**以下限制：** 所有资源管理器和高级事务管理器必须都支持事务\_通知\_回滚。

<a href="" id="transaction-notify-recover"></a>事务\_通知\_恢复  
**发送时**:资源管理器调用[ **ZwRecoverResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverresourcemanager)。

**收到的**:资源管理器。

**接收方所需的操作**:资源管理器必须调用[ **ZwRecoverEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverenlistment)。 (有关恢复操作的详细信息，请参阅[处理恢复操作](handling-recovery-operations.md)。)

**以下限制：** 无。

<a href="" id="transaction-notify-last-recover"></a>事务\_通知\_最后一个\_恢复  
**发送时**:KTM 已发送的最后一个事务之后\_通知\_恢复资源管理器的登记。

**收到的**:资源管理器。

**接收方所需的操作**:结束恢复操作。 (有关恢复操作的详细信息，请参阅[处理恢复操作](handling-recovery-operations.md)。)

**以下限制：** 无。

<a href="" id="transaction-notify-indoubt"></a>事务\_通知\_INDOUBT  
**发送时**:资源管理器会调用后[ **ZwRecoverEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverenlistment)，如果 KTM 无法确定是否应提交或回滚事务 (通常因为 TPS 具有上级事务管理器这是不可用）。

由接收：资源管理器。

**接收方所需的操作**:不执行任何操作之前 KTM 发送事务\_通知\_提交或事务\_通知\_回滚。

**以下限制：** 无。

<a href="" id="transaction-notify-rm-disconnected"></a>事务\_通知\_RM\_已断开连接  
**发送时**:正在处理的单阶段提交操作的资源管理器关闭而不指示它已提交或回滚该事务的登记句柄。

**收到的**:资源管理器和高级事务管理器具有事务的登记。

**接收方所需的操作**:特定于事务的清理操作。 通常情况下，此通知可为只读的资源管理器。

**以下限制：** 无。

### <a href="" id="notifications-for-superior-transaction-managers"></a> 高级事务管理器通知

[高级事务管理器](creating-a-superior-transaction-manager.md)可以接收以下通知：

<a href="" id="transaction-notify-rollback"></a>事务\_通知\_回滚  
请参阅前面的说明。

<a href="" id="transaction-notify-rm-disconnected"></a>事务\_通知\_RM\_已断开连接  
请参阅前面的说明。

<a href="" id="transaction-notify-preprepare-complete"></a>事务\_通知\_PREPREPARE\_完成  
**发送时**:所有资源管理器已收到事务\_通知\_PREPREPARE 和响应通过调用[ **ZwPrePrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepreparecomplete)。

**收到的**:高级事务管理器。

**接收方所需的操作**:上级事务管理器应调用[ **ZwPrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepareenlistment)。

<a href="" id="transaction-notify-prepare-complete"></a>事务\_通知\_准备\_完成  
**发送时**:所有资源管理器已收到事务\_通知\_准备和响应通过调用[ **ZwPrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreparecomplete)。

**收到的**:高级事务管理器。

**接收方所需的操作**:上级事务管理器应调用[ **ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)。

<a href="" id="transaction-notify-commit-complete"></a>事务\_通知\_提交\_完成  
**发送时**:所有资源管理器已收到事务\_通知\_提交，并通过调用响应[ **ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitcomplete)。

**收到的**:高级事务管理器。

**接收方所需的操作**:事务清理操作。

<a href="" id="transaction-notify-rollback-complete"></a>事务\_通知\_回滚\_完成  
**发送时**:所有资源管理器已收到事务\_通知\_回滚并响应通过调用[ **ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackcomplete)。

**收到的**:高级事务管理器。

**接收方所需的操作**:事务清理操作。

<a href="" id="transaction-notify-recover-query"></a>事务\_通知\_恢复\_查询  
**发送时**:上级事务管理器调用[ **ZwRecoverResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecoverresourcemanager)。

**收到的**:高级事务管理器。

**接收方所需的操作**:上级事务管理器必须调用[ **ZwCommitEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)或[ **ZwRollbackEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackenlistment)登记。

<a href="" id="transaction-notify-commit-request"></a>事务\_通知\_提交\_请求  
**发送时**:在客户端调用[ **ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)。 KTM 上级事务管理器已注册的登记此通知，如果将事务发送\_通知\_提交\_上级事务管理器对请求**而不是**发送事务\_通知\_提交到资源管理器。

**收到的**:高级事务管理器。

**接收方所需的操作**:高级事务管理器调用[ **ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)。

<a href="" id="transaction-notify-request-outcome"></a>事务\_通知\_请求\_结果  
**发送时**:资源管理器调用[ **TmRequestOutcomeEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmrequestoutcomeenlistment)时的事务处于准备好的状态。

**收到的**:高级事务管理器。

**接收方所需的操作**:上级事务管理器必须调用[ **ZwCommitEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)或[ **ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackenlistment)。

### <a href="" id="unused-notifications"></a> 未使用的通知

以下通知定义中 Ktmtypes.h，但 KTM 目前不支持它们：

事务\_通知\_委托\_提交

事务\_通知\_登记\_掩码

事务\_通知\_登记\_PREPREPARE

事务\_通知\_封送

事务\_通知\_提升

事务\_通知\_PROMOTE\_新建

事务\_通知\_传播\_拉取

事务\_通知\_传播\_推送

事务\_通知\_TM\_联机

事务\_通知\_提交\_FINALIZE

 

 




