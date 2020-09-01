---
title: 创建高级事务管理器
description: 创建高级事务管理器
ms.assetid: 6f6bf61a-fe53-47b5-9559-f76334969af8
keywords:
- 事务管理器 WDK KTM
- 高级事务管理器 WDK KTM
- 登记 WDK KTM，上级登记
- 上级登记 WDK KTM
- 登记 WDK KTM，从属登记
- 从属登记 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e30ca0a8117646a76a86de7c6fe54d7abdb7866
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190081"
---
# <a name="creating-a-superior-transaction-manager"></a>创建高级事务管理器


在 KTM 中， *上级事务管理* 器是一个资源管理器，它为它所参与的事务创建高级的登记。 *上级登记*是一种登记，它向资源管理器授予协调登记的事务的[提交操作](handling-commit-operations.md)的能力。 换句话说，事务客户端或上级事务管理器可以启动事务的预准备/准备/提交序列。

资源管理器为事务创建了上级登记后，KTM 拒绝对 [**ZwCommitTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommittransaction) 的所有调用。 因此，事务客户端无法提交此类事务。 创建上级登记的资源管理器必须调用 [**ZwPrePrepareEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)、 [**ZwPrepareEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)和 [**ZwCommitEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment)。

### <a name="when-to-create-a-superior-transaction-manager"></a>何时创建上级事务管理器

假设你想要将事务处理系统 (TPS 与 KTM) 组件相集成，但该组件包含了客户端可以调用的非 KTM 事务管理功能。 在这种情况下，您可能必须创建高级事务管理器。

例如，假设组件提供自己的接口，客户端使用这些接口来创建和提交事务。 由于组件的客户端不调用 KTM 来创建或提交事务，因此，在将组件集成到基于 KTM 的 TPS 时，组件必须成为上级事务管理器。

### <a name="how-to-create-a-superior-transaction-manager"></a>如何创建高级事务管理器

如果你希望组件成为上级事务管理器，则必须执行以下操作：

1.  调用 [**ZwCreateResourceManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateresourcemanager) 以将其注册为资源管理器。

2.  当组件的客户端使用组件的客户端接口创建事务时，请调用 [**ZwCreateTransaction**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransaction) 。

3.  调用 [**ZwCreateEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment)，设置登记 \_ 上级标志，并同时指定登记 \_ 高级 \_ 权限和登记 \_ 从属 \_ 权限访问标志。

4.  当组件的客户端调用组件的客户端接口以提交事务时，请调用 [**ZwPrePrepareEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntpreprepareenlistment)、 [**ZwPrepareEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntprepareenlistment)和 [**ZwCommitEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcommitenlistment) 。

KTM 只允许每个事务有一个上级登记。 其他资源管理器可以创建其他登记。 这些登记被称为 *从属登记* ，因为它们无法启动提交操作。

若要回滚上级登记，上级事务管理器将调用 [**ZwRollbackEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrollbackenlistment)。

若要恢复上级登记，上级事务管理器将调用 [**ZwRecoverEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntrecoverenlistment)。

当高级事务管理器提交、回滚或恢复事务时，KTM 会将 [事务通知](transaction-notifications.md) 发送到所有从属登记，使其可以参与。

包含上级事务管理器的 TPS 不能使用 [单阶段提交操作](handling-commit-operations.md#single-phase-commit-operations)。

在恢复操作过程中，如果 KTM 无法确定事务的结果，则会将事务 \_ 通知 \_ 恢复 \_ 查询通知发送到上级事务管理器。 在响应中，如果事务可以提交，则上级事务管理器必须调用 **ZwCommitEnlistment** ，如果应回滚事务，则必须 **ZwRollbackEnlistment** 。 如果上级事务管理器无法确定事务的结果，则它不应响应事务 \_ 通知 \_ 恢复 \_ 查询通知，直到它能够确定结果。

 

