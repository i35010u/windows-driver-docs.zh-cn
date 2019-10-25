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
ms.openlocfilehash: 0a425b3fddd5986e934b2d385eda2a8b9ba71257
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838384"
---
# <a name="transaction-notifications"></a>事务通知


KTM 为每个资源管理器提供通知队列。 KTM 将向资源管理器发送通知，方法是将其放在资源管理器的队列中。

资源管理器可以同步或异步地从其队列中检索通知。

-   若要同步检索通知，资源管理器可以重复调用[**ZwGetNotificationResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntgetnotificationresourcemanager)。

-   若要异步接收通知，资源管理器可以调用[**TmEnableCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmenablecallbacks)来设置回调例程。 每次向资源管理器的队列中放置一个通知时，KTM 都将调用回调例程。

当资源管理器调用[**ZwCreateEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)为事务创建登记时，资源管理器将指定它应收到的通知的类型。 资源管理器仅接收他们注册接收的通知。

通知常量在 Ktmtypes 中定义。 通知常量名称的格式为 TRANSACTION\_通知\_*Xxx*。

本主题的其余部分列出了 Ktmtypes 定义的所有通知常量，并将其划分为三个组：

-   资源管理器可以接收的通知

-   高级事务管理器可以接收的通知

-   定义但当前未使用的通知常量

### <a href="" id="notifications-for-resource-managers"></a>资源管理器的通知

所有资源管理器都必须注册以接收事务\_通知\_PREPREPARE、事务\_通知\_PREPARE 和 TRANSACTION\_通知\_提交通知，即使他们随后调用[**ZwReadOnlyEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntreadonlyenlistment)将登记标记为只读。

资源管理器可以支持事务\_通知\_单\_阶段\_提交，但他们还必须支持多阶段预准备、准备和提交通知。

下面的列表包含资源管理器可以接收的所有通知：

<a href="" id="transaction-notify-preprepare"></a>TRANSACTION\_通知\_PREPREPARE  
**发送时**：客户端调用[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction) ，而资源管理器不支持单阶段提交，或者如果[上级事务管理器](creating-a-superior-transaction-manager.md)调用[**ZwPrePrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)，则为。

**接收者**：资源管理器。

**收件人的所需操作**：执行预准备操作，然后调用[**ZwPrePrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)。 （有关预准备操作的详细信息，请参阅[处理提交操作](handling-commit-operations.md)。）

**限制：** 资源管理器还必须支持事务\_通知\_准备和事务\_通知提交\_。

<a href="" id="transaction-notify-prepare"></a>事务\_通知\_准备  
**当发送时**： TRANSACTION\_通知\_PREPREPARE 如果客户端调用[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction) ，并且没有资源管理器支持单阶段提交，或者上级事务管理器调用[**ZwPrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)。

**接收者**：资源管理器。

**收件人的必需操作：** 执行准备操作，然后调用[**ZwPrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)。 （有关准备操作的详细信息，请参阅[处理提交操作](handling-commit-operations.md)。）

**限制：** 资源管理器还必须支持事务\_通知\_PREPREPARE 和事务\_通知提交\_。

<a href="" id="transaction-notify-commit"></a>事务\_通知\_提交  
**发送时间**：如果客户端调用[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction) ，但没有资源管理器支持单阶段提交，或者上级事务管理器调用[**ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)，则 TRANSACTION\_会\_通知。

**接收者**：资源管理器。

**收件人的必需操作**：执行提交操作，然后调用[**ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)。 （有关提交操作的详细信息，请参阅[处理提交操作](handling-commit-operations.md)。）

**限制：** 资源管理器还必须支持事务\_通知\_PREPREPARE 和事务\_通知\_准备。

<a href="" id="transaction-notify-single-phase-commit"></a>事务\_通知\_单\_阶段\_提交  
**发送时**：客户端调用[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction) ，资源管理器支持单阶段提交操作。

**接收者**：资源管理器。

**收件人的所需操作**：提交事务或调用[**ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)。 （有关单阶段提交操作的详细信息，请参阅[处理提交操作](handling-commit-operations.md)。）

**限制：** 资源管理器还必须支持事务\_通知\_PREPREPARE、事务\_通知\_准备，以及事务\_通知\_提交。

<a href="" id="transaction-notify-rollback"></a>事务\_通知\_回滚  
**发送时**：客户端调用[**ZwRollbackTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbacktransaction)，上级事务管理器调用[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)，或 KTM 检测到错误（例如，写入日志流失败）。

**接收者**：资源管理器和上级事务管理器。

**接收方所需的操作**：执行回滚事务数据所需的任何操作，然后调用[**ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)。 （有关回滚操作的详细信息，请参阅[处理回滚操作](handling-rollback-operations.md)。）

**限制：** 所有资源管理器和上级事务管理器都必须支持事务\_通知\_回滚。

<a href="" id="transaction-notify-recover"></a>事务\_通知\_恢复  
**发送时间**：资源管理器调用[**ZwRecoverResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)。

**接收者**：资源管理器。

**收件人的必需操作**：资源管理器必须调用[**ZwRecoverEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment)。 （有关恢复操作的详细信息，请参阅[处理恢复操作](handling-recovery-operations.md)。）

**限制：** 内容.

<a href="" id="transaction-notify-last-recover"></a>事务\_通知\_上次\_恢复  
**发送时间**： KTM 发送了最后一个事务后\_通知资源管理器的登记\_恢复。

**接收者**：资源管理器。

**收件人的必需操作**：结束恢复操作。 （有关恢复操作的详细信息，请参阅[处理恢复操作](handling-recovery-operations.md)。）

**限制：** 内容.

<a href="" id="transaction-notify-indoubt"></a>TRANSACTION\_通知\_INDOUBT  
**发送时间**：在资源管理器调用[**ZwRecoverEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment)之后，如果 KTM 无法确定是否应提交或回滚事务（通常是因为该 TPS 的事务管理器不可用）。

接收者：资源管理器。

**接收方所需的操作**：不执行任何操作，除非 KTM 发送事务\_通知\_提交或事务\_通知\_回滚。

**限制：** 内容.

<a href="" id="transaction-notify-rm-disconnected"></a>\_通知\_RM\_断开连接  
**发送时**：正在处理单阶段提交操作的资源管理器会关闭登记句柄，而不表示它已提交或回滚事务。

**接收者**：具有事务登记的资源管理器和上级事务管理器。

**接收方的必需操作**：特定于事务的清理操作。 通常，此通知对只读资源管理器非常有用。

**限制：** 内容.

### <a href="" id="notifications-for-superior-transaction-managers"></a>上级事务管理器的通知

[上级事务管理器](creating-a-superior-transaction-manager.md)可能会收到以下通知：

<a href="" id="transaction-notify-rollback"></a>事务\_通知\_回滚  
请参阅前面的说明。

<a href="" id="transaction-notify-rm-disconnected"></a>\_通知\_RM\_断开连接  
请参阅前面的说明。

<a href="" id="transaction-notify-preprepare-complete"></a>事务\_通知\_PREPREPARE\_完成  
**发送时间**：在所有资源管理器接收到 TRANSACTION 后\_通过调用[**ZWPREPREPARECOMPLETE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)通知\_PREPREPARE 并做出响应。

**接收者**：优质事务管理器。

**收件人的必需操作**：上级事务管理器应调用[**ZwPrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)。

<a href="" id="transaction-notify-prepare-complete"></a>事务\_通知\_准备\_完成  
**发送时间**：在所有资源管理器都接收到 TRANSACTION 后\_通过调用[**ZWPREPARECOMPLETE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)通知\_准备并做出响应。

**接收者**：优质事务管理器。

**收件人的必需操作**：上级事务管理器应调用[**ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)。

<a href="" id="transaction-notify-commit-complete"></a>事务\_通知\_提交\_完成  
**发送时间**：在所有资源管理器收到 TRANSACTION 后\_通过调用[**ZWCOMMITCOMPLETE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)通知\_提交并做出响应。

**接收者**：优质事务管理器。

**收件人的必需操作**：事务清理操作。

<a href="" id="transaction-notify-rollback-complete"></a>事务\_通知\_回滚\_完成  
**发送时间**：在所有资源管理器收到 TRANSACTION 后\_通过调用[**ZWROLLBACKCOMPLETE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)通知\_回滚并做出响应。

**接收者**：优质事务管理器。

**收件人的必需操作**：事务清理操作。

<a href="" id="transaction-notify-recover-query"></a>TRANSACTION\_通知\_RECOVER\_查询  
**发送时间**：上级事务管理器调用[**ZwRecoverResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)。

**接收者**：优质事务管理器。

**收件人的必需操作**：上级事务管理器必须调用[**ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)或[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)来进行登记。

<a href="" id="transaction-notify-commit-request"></a>事务\_通知\_提交\_请求  
**发送时**：客户端调用[**ZwCommitTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction)。 如果上级事务管理器已为登记注册了此通知，则 KTM 将发送事务\_通知\_COMMIT\_请求发送到上级事务管理器，**而不是**发送事务\_通知\_提交给资源管理器。

**接收者**：优质事务管理器。

**收件人的必需操作**：上级事务管理器调用[**ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)。

<a href="" id="transaction-notify-request-outcome"></a>事务\_通知\_请求\_结果  
**发送时**：资源管理器会在事务处于准备就绪状态时调用[**TmRequestOutcomeEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmrequestoutcomeenlistment) 。

**接收者**：优质事务管理器。

**收件人的必需操作**：上级事务管理器必须调用[**ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)或[**ZwRollbackEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)。

### <a href="" id="unused-notifications"></a>未使用通知

以下通知是在 Ktmtypes 中定义的，但 KTM 当前不支持它们：

事务\_通知\_委托\_提交

\_通知\_登记\_掩码

事务\_通知\_登记\_PREPREPARE

事务\_通知\_封送

事务\_通知\_升级

事务\_通知\_提升\_新

事务\_通知\_传播\_请求

事务\_通知\_传播\_推送

事务\_\_TM\_联机通知

事务\_通知\_提交\_FINALIZE

 

 




