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
ms.openlocfilehash: 149d9568561723053854137aa796585b0de43b63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838654"
---
# <a name="handling-recovery-operations"></a>处理恢复操作


在*恢复*操作中，事务处理系统（TPS）尝试从[日志流](using-log-streams-with-ktm.md)中的信息恢复其状态。 恢复操作完成后，所有事务都应处于已提交或已回滚状态，并且所有资源数据应处于已知的良好状态。

有时，TPS 会在其所有事务完成之前停止。 例如，操作系统可能会崩溃。 因此，资源管理器必须在启动时启动恢复操作。 恢复操作将尝试确定是否有任何事务未完成。 如果在日志中找到了不完整的事务，则恢复操作将尝试提交或回滚这些事务。

对于基于 KTM 的 TPS，每个恢复操作都包含两个步骤。 第一步是从事务管理器对象的日志流中恢复信息。 第二步涉及到从资源管理器的日志流中恢复信息。

TPS 可以恢复到所有日志流的末尾，或者，如果其资源管理器维护[虚拟时钟值](using-virtual-clock-values.md)，则它可以恢复到指定的时钟值。

### <a name="recovering-information-from-a-transaction-manager-objects-log-stream"></a>从事务管理器对象的日志流中恢复信息

资源管理器在调用[**ZwCreateTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)或[**ZwOpenTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransactionmanager)后立即调用[**ZwRecoverTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)。 **ZwRecoverTransactionManager**例程读取属于事务管理器对象的日志流。 此例程会从该日志流中的恢复信息重新构造事务管理器对象（包括所有事务、登记和资源管理器）的状态，从 KTM 创建的上一个[重新开始区域](reading-restart-records-from-a-clfs-stream.md)开始，在流的末尾结束。

若要从上一次重新启动区域恢复到指定的虚拟时钟值，资源管理器可以调用[**ZwRollforwardTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollforwardtransactionmanager)而不是**ZwRecoverTransactionManager**。

### <a name="recovering-information-from-a-resource-managers-log-stream"></a>从资源管理器的日志流中恢复信息

资源管理器在调用[**ZwCreateResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager)或[**ZwOpenResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenresourcemanager)后立即调用[**ZwRecoverResourceManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverresourcemanager)。 **ZwRecoverResourceManager**例程尝试恢复与每个资源管理器的登记关联的事务。

当资源管理器调用**ZwRecoverResourceManager**时，KTM 将发送事务\_通知每个资源管理器的登记\_恢复[通知](transaction-notifications.md)。 资源管理器必须在每次收到其中一个事务\_通知\_恢复通知时调用[**ZwRecoverEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment) 。

当资源管理器调用**ZwRecoverEnlistment**时，KTM 将发送以下通知之一：

-   事务\_通知\_提交

    资源管理器必须使用其日志流中的信息来提交事务，然后必须调用[**ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)。

-   事务\_通知\_回滚

    资源管理器必须使用其日志流中的信息来回滚事务，然后必须调用[**ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)。

-   TRANSACTION\_通知\_INDOUBT

    KTM 未确定事务的状态，稍后将发送 commit 或 rollback 通知。

通常，当 KTM 确定 ZwPrepareComplete 在该 TPS 停止并重新启动之前调用了 " [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete) " 时，它会发送事务\_通知\_提交通知。 如果 ZwPrepareComplete 确定一个或多个资源管理器未调用，则 KTM 发送事务\_通知\_回滚通知。

当 KTM 发送事务\_通知每个登记\_恢复通知时，它会发送一个事务\_\_通知最后\_恢复通知。

如果资源管理器调用**ZwRollforwardTransactionManager**而不是**ZwRecoverTransactionManager**，则它必须仅恢复到它指定给**ZwRollforwardTransactionManager**的虚拟时钟值。

资源管理器可以调用[**ZwSetInformationEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsetinformationenlistment)来设置自定义的恢复信息。 KTM 保存此信息并将其写入日志流，但 KTM 不尝试解释信息。 资源管理器可以通过调用[**ZwQueryInformationEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationenlistment)随时检索恢复信息。

[高级事务管理器](creating-a-superior-transaction-manager.md)有时会接收事务\_在恢复操作期间通知\_恢复\_查询通知。

 

 




