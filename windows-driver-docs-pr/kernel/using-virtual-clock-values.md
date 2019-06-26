---
title: 使用虚拟时钟值
description: 使用虚拟时钟值
ms.assetid: de01b0f1-86b1-4e7d-af22-84dbbe3a3f83
keywords:
- 虚拟时钟值 WDK KTM
- 内核事务管理器 WDK，虚拟时钟值
- KTM WDK，虚拟时钟值
- 事务 WDK KTM，虚拟时钟值
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ffa11c5e97266a5224aada8f99b8ca1628d8614
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358160"
---
# <a name="using-virtual-clock-values"></a>使用虚拟时钟值


KTM 提供虚拟时钟为每个事务管理器对象。 当资源管理器调用[ **ZwCreateTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransactionmanager)，KTM 对象的虚拟时钟值设置为 1。 KTM 虚拟时钟值增加每个提交操作开始的时间。 每当 KTM 写入其日志流，它将包括当前虚拟时钟值中的日志记录。

当资源管理器调用[ **ZwRecoverTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrecovertransactionmanager)、 KTM 读取日志流记录的流的结束之前，和它的事务管理器对象的虚拟时钟值设置为最后一个值在对象的日志流中查找它。

当资源管理器调用[ **ZwRollforwardTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollforwardtransactionmanager)、 KTM 读取日志流记录，直到达到指定的时钟值，和它的事务管理器对象的虚拟时钟值设置为指定的时钟值。

KTM 使资源管理器和高级事务管理器可修改的事务管理器对象虚拟时钟值，但它们通常不需要修改的时钟值。

### <a name="when-to-modify-virtual-clock-values"></a>何时修改虚拟时钟值

通常情况下，在事务处理系统 (TPS) 无需修改虚拟时钟值，除非在 TP 中的组件试图将多个日志流同步。

例如，假设你 TP 包含在前-prepare/准备/提交序列期间与彼此通信的多个资源管理器。 此外假设每个资源管理器创建具有唯一的日志流的事务管理器对象。 若要确保，KTM 还原状态的所有资源管理器到同一点及时恢复操作期间，这些资源管理器可以使用以下步骤：

-   如果一个资源管理器通信与另一个，请将传递它已收到来自任一 KTM 的最新虚拟时钟值或另一个资源管理器。

-   每当资源管理器调用接受虚拟时钟值的 KTM 例程 （请参阅本主题中的以下部分），它将传递它已收到来自 KTM 或另一个资源管理器的最大时钟值。

-   每个资源管理器将虚拟时钟值写入到其日志的流，并执行回滚或恢复操作时使用这些值。

这些步骤会导致虚拟时钟值 KTM 存储到每个事务管理器对象的几乎或完全匹配。 因此，恢复操作会导致 KTM 读取其日志流，或回滚操作会导致资源管理器来读取其日志流时，恢复或回滚基于同步的日志流。

### <a name="how-to-modify-virtual-clock-values"></a>如何修改虚拟时钟值

资源管理器可以通过传递到新值来修改虚拟时钟值[ **ZwPrePrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepreparecomplete)， [ **ZwPrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreparecomplete)，[ **ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitcomplete)， [ **ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbackcomplete)， [ **ZwReadOnlyEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntreadonlyenlistment)，或[ **ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntsinglephasereject)。

[高级事务管理器](creating-a-superior-transaction-manager.md)可以通过传递到一个新值来修改虚拟时钟值[ **ZwPrePrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntpreprepareenlistment)， [ **ZwPrepareEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntprepareenlistment)， [ **ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommitenlistment)，或者[ **ZwReadOnlyEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntreadonlyenlistment)。

此外，资源管理器或上级事务管理器，它使用[ **ResourceManagerNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ptm_rm_notification)回调例程可以修改回调例程接收虚拟时钟值。 KTM 然后保存更新后的值。

如果资源管理器或上级事务管理器将新的时钟值传递到 KTM，KTM 将保存新值，仅当其值大于当前时钟值。 否则，KTM 中保留当前时钟值。

资源管理器和高级事务管理器可以获取事务管理器对象的虚拟时钟值通过调用[ **ZwQueryInformationTransactionManager** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransactionmanager)例程。

 

 




