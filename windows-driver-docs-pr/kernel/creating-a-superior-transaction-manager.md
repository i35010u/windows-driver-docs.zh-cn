---
title: 创建高级事务管理器
description: 创建高级事务管理器
ms.assetid: 6f6bf61a-fe53-47b5-9559-f76334969af8
keywords:
- 事务管理器 WDK KTM
- 高级事务管理器 WDK KTM
- 登记 WDK KTM，高级登记
- 高级登记 WDK KTM
- 登记 WDK KTM，从属登记
- 从属登记 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25f9ba7163ef8816fc8cdbb1e83be7b741ed0cdf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345439"
---
# <a name="creating-a-superior-transaction-manager"></a>创建高级事务管理器


KTM，在*上级事务管理器*创建卓越的登记其参与的事务的资源管理器。 一个*上级登记*是授予资源管理器的功能进行协调的登记[提交操作](handling-commit-operations.md)登记的事务。 换而言之，事务的客户端或上级事务管理器可以启动的事务前的 prepare/准备/提交序列。

KTM 的资源管理器创建一个事务是上级登记后，会拒绝所有调用的[ **ZwCommitTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff566420)事务。 因此，事务的客户端不能提交此类的新事务。 相反，必须调用创建上级登记的资源管理器[ **ZwPrePrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567044)， [ **ZwPrepareEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff567039)，并[ **ZwCommitEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff566419)。

### <a name="when-to-create-a-superior-transaction-manager"></a>何时创建上级事务管理器

假设你想要将事务处理系统 (TPS) 组件与 KTM，但该组件包含客户端可以调用其自身非 KTM 事务管理功能。 在这种情况下，可能需要创建高级事务管理器。

例如，假设您的组件提供了它自己的客户端用于创建和提交事务的接口。 组件的客户端不调用 KTM 创建或提交事务，因为你的组件必须成为上级事务管理器时将其集成到基于 KTM 的 TP。

### <a name="how-to-create-a-superior-transaction-manager"></a>如何创建出色的事务管理器

如果你想让组件能够成为高级事务管理器，它必须执行以下操作：

1.  调用[ **ZwCreateResourceManager** ](https://msdn.microsoft.com/library/windows/hardware/ff566427)注册为资源管理器。

2.  调用[ **ZwCreateTransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff566429)每次你的组件的客户端使用组件的客户端接口创建一个事务。

3.  调用[ **ZwCreateEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff566422)，设置登记\_卓越标志，并指定这两个登记\_上级\_权限和登记\_从属\_权限访问标志。

4.  调用[ **ZwPrePrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567044)， [ **ZwPrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567039)，并[ **ZwCommitEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff566419)组件的客户端时调用组件的客户端接口来提交事务。

KTM 允许只有一个上级登记每个事务。 其他资源管理器可以创建其他的登记。 调用这些登记*从属登记*因为它们不能启动提交操作。

若要回滚上级登记，高级事务管理器调用[ **ZwRollbackEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567083)。

若要恢复上级登记，高级事务管理器调用[ **ZwRecoverEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567075)。

当上级事务管理器提交、 回滚，或恢复事务时，将发送 KTM[事务通知](transaction-notifications.md)，以便它们可以加入，则所有从属的登记。

不能使用包括上级事务管理器的 TP[单阶段提交操作](handling-commit-operations.md#single-phase-commit-operations)。

在恢复操作中，如果 KTM 无法确定结果的事务，则会发送事务\_通知\_恢复\_到上级事务管理器的查询通知。 在响应中，必须调用上级事务管理器**ZwCommitEnlistment**如果可以提交事务或**ZwRollbackEnlistment**如果应回滚事务。 如果上级事务管理器无法确定事务的结果，它应不响应的事务\_通知\_恢复\_查询通知，直到它可以确定结果。

 

 




