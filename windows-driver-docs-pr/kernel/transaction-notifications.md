---
title: 事务通知
description: 事务通知
ms.assetid: 62169b56-e70f-4d32-a051-a7fd947dbc64
keywords:
- 通知 WDK KTM
- 事务 WDK KTM，通知
- 资源管理器 WDK KTM，通知
- 内核事务管理器 WDK，通知
- KTM WDK，通知
- 高级事务管理器 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b437d9448169396b0dbf52eba601c3b832c1d7af
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189777"
---
# <a name="transaction-notifications"></a>事务通知


KTM 为每个资源管理器提供通知队列。 KTM 将向资源管理器发送通知，方法是将其放在资源管理器的队列中。

资源管理器可以同步或异步地从其队列中检索通知。

-   若要同步检索通知，资源管理器可以重复调用 [**ZwGetNotificationResourceManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntgetnotificationresourcemanager)。

-   若要异步接收通知，资源管理器可以调用 [**TmEnableCallbacks**](/windows-hardware/drivers/ddi/wdm/nf-wdm-tmenablecallbacks) 来设置回调例程。 每次向资源管理器的队列中放置一个通知时，KTM 都将调用回调例程。

当资源管理器调用 [**ZwCreateEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment) 为事务创建登记时，资源管理器将指定它应收到的通知的类型。 资源管理器仅接收他们注册接收的通知。

通知常量在 Ktmtypes 中定义。 通知常量名称的格式为事务 \_ 通知 \_ *Xxx*。

本主题的其余部分列出了 Ktmtypes 定义的所有通知常量，并将其划分为三个组：

-   资源管理器可以接收的通知

-   高级事务管理器可以接收的通知

-   定义但当前未使用的通知常量

### <a name="notifications-for-resource-managers"></a><a href="" id="notifications-for-resource-managers"></a> 资源管理器的通知

所有资源管理器都必须注册以接收事务通知 \_ \_ PREPREPARE、事务 \_ 通知 \_ 准备和事务 \_ 通知 \_ 提交通知，即使它们随后调用 [**ZwReadOnlyEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntreadonlyenlistment) 将登记标记为只读。

资源管理器可以支持事务 \_ 通知 \_ 单 \_ 阶段 \_ 提交，但必须支持多阶段预准备、准备和提交通知。

下面的列表包含资源管理器可以接收的所有通知：

<a href="" id="transaction-notify-preprepare"></a>事务 \_ 通知 \_ PREPREPARE  
**发送时**：客户端调用 [**ZwCommitTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction) ，而资源管理器不支持单阶段提交，或者如果 [上级事务管理器](creating-a-superior-transaction-manager.md) 调用 [**ZwPrePrepareEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)，则为。

**接收者**：资源管理器。

**收件人的所需操作**：执行预准备操作，然后调用 [**ZwPrePrepareComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)。  (有关预准备操作的详细信息，请参阅 [处理提交操作](handling-commit-operations.md)。 ) 

**限制：** 资源管理器还必须支持事务 \_ 通知 \_ 准备和事务 \_ 通知 \_ 提交。

<a href="" id="transaction-notify-prepare"></a>事务 \_ 通知 \_ 准备  
**发送时间**： \_ \_ 如果客户端调用 [**ZwCommitTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction) ，并且没有资源管理器支持单阶段提交，或者上级事务管理器调用 [**ZwPrepareEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)，则在事务通知之后 PREPREPARE。

**接收者**：资源管理器。

**收件人的必需操作：** 执行准备操作，然后调用 [**ZwPrepareComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)。  (有关准备操作的详细信息，请参阅 [处理提交操作](handling-commit-operations.md)。 ) 

**限制：** 资源管理器还必须支持事务 \_ 通知 \_ PREPREPARE 和事务 \_ 通知 \_ 提交。

<a href="" id="transaction-notify-commit"></a>事务 \_ 通知 \_ 提交  
**发送时间**： \_ \_ 如果客户端调用 [**ZwCommitTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction) ，但没有资源管理器支持单阶段提交，或者上级事务管理器调用 [**ZwCommitEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)，则在事务通知完成之后进行准备。

**接收者**：资源管理器。

**收件人的必需操作**：执行提交操作，然后调用 [**ZwCommitComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)。  (有关提交操作的详细信息，请参阅 [处理提交操作](handling-commit-operations.md)。 ) 

**限制：** 资源管理器还必须支持事务 \_ 通知 \_ PREPREPARE 和事务 \_ 通知 \_ 准备。

<a href="" id="transaction-notify-single-phase-commit"></a>事务 \_ 通知 \_ 单 \_ 阶段 \_ 提交  
**发送时**：客户端调用 [**ZwCommitTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction) ，资源管理器支持单阶段提交操作。

**接收者**：资源管理器。

**收件人的所需操作**：提交事务或调用 [**ZwSinglePhaseReject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)。  (有关单阶段提交操作的详细信息，请参阅 [处理提交操作](handling-commit-operations.md)。 ) 

**限制：** Resource manager 还必须支持事务 \_ 通知 \_ PREPREPARE、事务 \_ 通知 \_ 准备和事务 \_ 通知 \_ 提交。

<a href="" id="transaction-notify-rollback"></a>事务 \_ 通知 \_ 回滚  
**发送时**：客户端调用 [**ZwRollbackTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction)，上级事务管理器调用 [**ZwRollbackEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)，或 KTM 检测到错误 (例如写入日志流) 失败。

**接收者**：资源管理器和上级事务管理器。

**接收方所需的操作**：执行回滚事务数据所需的任何操作，然后调用 [**ZwRollbackComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)。  (有关回滚操作的详细信息，请参阅 [处理回滚操作](handling-rollback-operations.md)。 ) 

**限制：** 所有资源管理器和上级事务管理器都必须支持事务 \_ 通知 \_ 回滚。

<a href="" id="transaction-notify-recover"></a>事务 \_ 通知 \_ 恢复  
**发送时间**：资源管理器调用 [**ZwRecoverResourceManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)。

**接收者**：资源管理器。

**收件人的必需操作**：资源管理器必须调用 [**ZwRecoverEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment)。  (有关恢复操作的详细信息，请参阅 [处理恢复操作](handling-recovery-operations.md)。 ) 

**限制：** 无。

<a href="" id="transaction-notify-last-recover"></a>事务 \_ 通知 \_ 上次 \_ 恢复  
**发送时**： KTM 发送了 \_ \_ 资源管理器的登记的上一个事务通知恢复。

**接收者**：资源管理器。

**收件人的必需操作**：结束恢复操作。  (有关恢复操作的详细信息，请参阅 [处理恢复操作](handling-recovery-operations.md)。 ) 

**限制：** 无。

<a href="" id="transaction-notify-indoubt"></a>事务 \_ 通知 \_ INDOUBT  
**发送时间**：在资源管理器调用 [**ZwRecoverEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment)之后，如果 KTM 无法确定是否应提交或回滚事务 (通常是因为该 TPS 具有一个不可用) 的上级事务管理器。

接收者：资源管理器。

**接收方所需的操作**：不执行任何操作，直到 KTM 发送事务 \_ 通知 \_ 提交或事务 \_ 通知 \_ 回滚。

**限制：** 无。

<a href="" id="transaction-notify-rm-disconnected"></a>事务 \_ 通知 \_ RM 已 \_ 断开连接  
**发送时**：正在处理单阶段提交操作的资源管理器会关闭登记句柄，而不表示它已提交或回滚事务。

**接收者**：具有事务登记的资源管理器和上级事务管理器。

**接收方的必需操作**：特定于事务的清理操作。 通常，此通知对只读资源管理器非常有用。

**限制：** 无。

### <a name="notifications-for-superior-transaction-managers"></a><a href="" id="notifications-for-superior-transaction-managers"></a> 上级事务管理器的通知

[上级事务管理器](creating-a-superior-transaction-manager.md) 可能会收到以下通知：

<a href="" id="transaction-notify-rollback"></a>事务 \_ 通知 \_ 回滚  
请参阅前面的说明。

<a href="" id="transaction-notify-rm-disconnected"></a>事务 \_ 通知 \_ RM 已 \_ 断开连接  
请参阅前面的说明。

<a href="" id="transaction-notify-preprepare-complete"></a>事务 \_ 通知 \_ PREPREPARE \_ 完成  
**发送时间**：在所有资源管理器收到 TRANSACTION \_ 通知 \_ PREPREPARE 并通过调用 [**ZwPrePrepareComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)进行响应之后。

**接收者**：优质事务管理器。

**收件人的必需操作**：上级事务管理器应调用 [**ZwPrepareEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)。

<a href="" id="transaction-notify-prepare-complete"></a>事务 \_ 通知 \_ 准备 \_ 完成  
**发送时间**：在所有资源管理器收到事务 \_ 通知时 \_ ，通过调用 [**ZwPrepareComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)进行准备并做出响应。

**接收者**：优质事务管理器。

**收件人的必需操作**：上级事务管理器应调用 [**ZwCommitEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)。

<a href="" id="transaction-notify-commit-complete"></a>事务 \_ 通知 \_ 提交 \_ 完成  
**发送时间**：在所有资源管理器收到事务 \_ 通知 \_ 提交并通过调用 [**ZwCommitComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)进行响应之后。

**接收者**：优质事务管理器。

**收件人的必需操作**：事务清理操作。

<a href="" id="transaction-notify-rollback-complete"></a>事务 \_ 通知 \_ 回滚 \_ 完成  
**发送时间**：在所有资源管理器收到事务 \_ 通知 \_ 回滚并通过调用 [**ZwRollbackComplete**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)进行响应之后。

**接收者**：优质事务管理器。

**收件人的必需操作**：事务清理操作。

<a href="" id="transaction-notify-recover-query"></a>事务 \_ 通知 \_ 恢复 \_ 查询  
**发送时间**：上级事务管理器调用 [**ZwRecoverResourceManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)。

**接收者**：优质事务管理器。

**收件人的必需操作**：上级事务管理器必须调用 [**ZwCommitEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment) 或 [**ZwRollbackEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment) 来进行登记。

<a href="" id="transaction-notify-commit-request"></a>事务 \_ 通知 \_ 提交 \_ 请求  
**发送时**：客户端调用 [**ZwCommitTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)。 如果上级事务管理器已为登记注册了此通知，则 KTM 会 \_ \_ \_ 向上级事务管理器发送事务通知提交请求， **而不是** 将事务 \_ 通知 \_ 提交发送到资源管理器。

**接收者**：优质事务管理器。

**收件人的必需操作**：上级事务管理器调用 [**ZwCommitEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)。

<a href="" id="transaction-notify-request-outcome"></a>事务 \_ 通知 \_ 请求 \_ 结果  
**发送时**：资源管理器会在事务处于准备就绪状态时调用 [**TmRequestOutcomeEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-tmrequestoutcomeenlistment) 。

**接收者**：优质事务管理器。

**收件人的必需操作**：上级事务管理器必须调用 [**ZwCommitEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment) 或 [**ZwRollbackEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)。

### <a name="unused-notifications"></a><a href="" id="unused-notifications"></a> 未使用通知

以下通知是在 Ktmtypes 中定义的，但 KTM 当前不支持它们：

事务 \_ 通知 \_ 委托 \_ 提交

事务 \_ 通知 \_ 登记 \_ 掩码

事务 \_ 通知 \_ 登记 \_ PREPREPARE

事务 \_ 通知 \_ 封送

事务 \_ 通知 \_ 升级

事务 \_ 通知 \_ 升级 \_ 新

事务 \_ 通知 \_ 传播 \_ 请求

事务 \_ 通知 \_ 传播 \_ 推送

事务 \_ 通知 \_ TM \_ ONLINE

事务 \_ 通知 \_ 提交 \_ 完成

 

