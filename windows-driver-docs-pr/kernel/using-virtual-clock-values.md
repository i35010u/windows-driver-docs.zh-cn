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
ms.openlocfilehash: ce58b80603856f2311357e66b621eba6c91fbba7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835816"
---
# <a name="using-virtual-clock-values"></a>使用虚拟时钟值


KTM 为每个事务管理器对象提供虚拟时钟。 当资源管理器调用[**ZwCreateTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)时，KTM 会将对象的虚拟时钟值设置为1。 每次提交操作开始时，KTM 会递增虚拟时钟值。 当 KTM 写入其日志流时，它会在日志记录中包含当前的虚拟时钟值。

当资源管理器调用[**ZwRecoverTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecovertransactionmanager)时，KTM 将读取日志流记录直到流的结尾，并将事务管理器对象的虚拟时钟值设置为它在对象的日志流中找到的最后一个值。

当资源管理器调用[**ZwRollforwardTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollforwardtransactionmanager)时，KTM 将读取日志流记录直到指定的时钟值，并将事务管理器对象的虚拟时钟值设置为指定的时钟值。

使用 KTM，资源管理器和上级事务管理器可以修改事务管理器对象的虚拟时钟值，但通常不需要修改时钟值。

### <a name="when-to-modify-virtual-clock-values"></a>何时修改虚拟时钟值

通常，你的事务处理系统（TPS）不需要修改虚拟时钟值，除非你的 TPS 中的组件尝试同步多个日志流。

例如，假设你的 TPS 包含多个资源管理器，它们会在准备/准备/提交序列过程中相互通信。 还假设每个资源管理器创建一个具有唯一日志流的事务管理器对象。 为了确保 KTM 在恢复操作过程中将所有资源管理器的状态恢复到相同的时间点，这些资源管理器可能需要执行以下步骤：

-   当一个资源管理器与另一个资源管理器进行通信时，它会传递从 KTM 或其他资源管理器接收的最新虚拟时钟值。

-   每当资源管理器调用接受虚拟时钟值的 KTM 例程（请参阅本主题中的以下部分）时，它会传递从 KTM 或其他资源管理器收到的最高时钟值。

-   每个资源管理器都将虚拟时钟值写入其日志流，并在执行回滚或恢复操作时使用这些值。

这些步骤导致 KTM 存储的每个事务管理器对象的虚拟时钟值几乎或完全匹配。 因此，当恢复操作使 KTM 读取其日志流时，或者当回滚操作导致资源管理器读取其日志流时，恢复或回滚基于已同步的日志流。

### <a name="how-to-modify-virtual-clock-values"></a>如何修改虚拟时钟值

资源管理器可以通过将新值传递到[**ZwPrePrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepreparecomplete)、 [**ZwPrepareComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreparecomplete)、 [**ZwCommitComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitcomplete)、 [**ZwRollbackComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackcomplete)、 [**ZwReadOnlyEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntreadonlyenlistment)或[**来修改虚拟时钟值ZwSinglePhaseReject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntsinglephasereject)。

[高级事务管理器](creating-a-superior-transaction-manager.md)可以通过将新值传递到[**ZwPrePrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)、 [**ZwPrepareEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)、 [**ZwCommitEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)或[**ZwReadOnlyEnlistment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntreadonlyenlistment)来修改虚拟时钟值。

此外，使用[**ResourceManagerNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ptm_rm_notification)回调例程的资源管理器或上级事务管理器可以修改回调例程收到的虚拟时钟值。 然后 KTM 保存更新的值。

如果资源管理器或上级事务管理器将新的时钟值传递给 KTM，则 KTM 仅在其大于当前时钟值时才保存新值。 否则，KTM 将保留当前时钟值。

资源管理器和上级事务管理器可以通过调用[**ZwQueryInformationTransactionManager**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ntqueryinformationtransactionmanager)例程来获取事务管理器对象的虚拟时钟值。

 

 




