---
title: 处理提交操作
description: 处理提交操作
ms.assetid: 4885476e-ce68-4674-b8a5-8a317f33cd5b
keywords:
- WDK KTM，提交事务的事务
- 提交事务 WDK KTM
- 资源管理器 WDK KTM，提交事务
- 单阶段提交 WDK KTM，多阶段提交 WDK KTM
- 预先准备阶段 WDK KTM
- 准备阶段 WDK KTM
- 提交阶段 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: da1a107f0ca554dfd91937148a39bdc68c20c0a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569441"
---
# <a name="handling-commit-operations"></a>处理提交操作


有两种类型的提交操作：*单阶段提交*并*多阶段提交*。 单阶段提交操作包含的多阶段提交操作包括的准备步骤的其他通知资源管理器必须做出响应，一条通知。

单阶段提交操作是实现变得简单。 它是适用于事务处理系统 (TPSs) 具有以下特征之一：

-   单个资源管理器。

-   多个资源管理器，其中的一个[只读](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)和提交操作不会加入。

如果多个资源管理器参与提交操作必须进行多阶段提交操作。

### <a name="single-phase-commit-operations"></a>使用单阶段提交操作

如果你想要支持单阶段提交操作在 TP，一个 （且只有一个） 资源管理器必须注册才能接收事务\_通知\_单个\_阶段\_提交[通知](transaction-notifications.md)其登记。 所有其他资源管理器必须是[只读](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)。

包括 TP[上级事务管理器](creating-a-superior-transaction-manager.md)不能使用单阶段提交。

如果资源管理器已注册为接收事务\_通知\_单个\_阶段\_提交通知 KTM 发送通知的此类事务的客户端调用时[ **ZwCommitTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff566420)。

当资源管理器收到事务\_通知\_单个\_阶段\_提交通知事务，它可以提交事务或拒绝单阶段提交。

若要提交事务，资源管理器必须执行以下步骤：

1.  刷新的非永久性缓存 （内存中存储） 中保存任何数据，如[封送处理区域 CLFS](clfs-marshalling-areas.md)有关[CLFS 日志流](using-log-streams-with-ktm.md)。

    资源管理器必须将数据从缓存移动到持久性存储介质。 例如，可以调用的资源管理器使用 CLFS [ **ClfsFlushBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff541544)。

2.  永久和公共进行所有数据更改 (即，资源管理器的作用域外可见)。

3.  调用[ **ZwCommitComplete**](https://msdn.microsoft.com/library/windows/hardware/ff566418)。

在调用**ZwCommitComplete**，应调用资源管理器[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)关闭登记句柄。

若要拒绝的事务的单阶段提交操作，资源管理器可以调用[ **ZwSinglePhaseReject**](https://msdn.microsoft.com/library/windows/hardware/ff567113)。 如果资源管理器调用**ZwSinglePhaseReject**，KTM 立即提交操作将从更改单阶段为多个阶段。

如果在同一事务中登记其他资源管理器，则必须在[只读](creating-a-resource-manager.md#kernel-creating-a-read-only-enlistment)。 但是，它们必须注册才能接收事务\_通知\_RM\_断开连接的通知，它们接收处理单阶段提交操作的资源管理器将关闭登记处理未指示它已提交或回滚事务。

### <a name="multi-phase-commit-operations"></a>使用多阶段提交操作

在多阶段提交操作开始时将发生以下事件之一：

-   事务的客户端调用[ **ZwCommitTransaction**](https://msdn.microsoft.com/library/windows/hardware/ff566420)，并没有资源管理器已注册接收事务\_通知\_单一\_阶段\_提交通知。

-   资源管理器调用[ **ZwSinglePhaseReject** ](https://msdn.microsoft.com/library/windows/hardware/ff567113)接收到一个事务之后\_通知\_单一\_阶段\_提交通知。

-   一个[上级事务管理器](creating-a-superior-transaction-manager.md)调用[ **ZwPrePrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567044)。

多阶段提交操作包括三个连续的阶段：*预先准备*，*准备*，并*提交*。

**预先准备阶段**

Pre-prepare 阶段 (也称为*阶段零*) 的提交操作开始时 KTM 发送事务\_通知\_PREPREPARE 通知到所有资源管理器。 KTM 发送此通知，如果没有资源管理器支持单阶段提交操作的事务，或如果上级事务管理器调用[ **ZwPrePrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567044)。

当每个资源管理器接收的事务\_通知\_PREPREPARE 通知时，它必须执行以下操作：

1.  刷新的非永久性缓存 （内存中存储） 中保存任何数据，如[封送处理区域 CLFS](clfs-marshalling-areas.md)有关[CLFS 日志流](using-log-streams-with-ktm.md)。

    资源管理器必须将数据从缓存移动到持久性存储介质。 例如，可以调用的资源管理器使用 CLFS [ **ClfsFlushBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff541544)。

2.  调用[ **ZwPrePrepareComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567040)。

后一个资源管理器调用了具有**ZwPreprepareComplete**，它可以继续接收和处理客户端请求。 但资源管理器必须将所有数据修改都视为缓存传递操作立即写入到持久性存储介质。

如果资源管理器遇到错误，正在进行的事务\_通知\_PREPREPARE 通知，则应调用[ **ZwRollbackEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff567083)回滚该事务。

**准备阶段**

在准备阶段 (也称为*第一阶段*) 的提交操作开始时 KTM 发送事务\_通知\_到所有资源管理器准备通知。 KTM 发送此通知后事务\_通知\_PREPREPARE 如果没有资源管理器支持单阶段提交或上级事务管理器会调用[ **ZwPrepareEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff567039).

当每个资源管理器接收的事务\_通知\_准备通知时，它必须执行以下操作：

1.  停止为客户端请求提供服务，并报告任何客户端为客户端错误的后续请求。

2.  请确保所有数据已被都移动到持久存储。

3.  调用[ **ZwPrepareComplete**](https://msdn.microsoft.com/library/windows/hardware/ff567037)。

如果资源管理器遇到错误，正在进行的事务\_通知\_准备通知，则应调用[ **ZwRollbackEnlistment** ](https://msdn.microsoft.com/library/windows/hardware/ff567083)回滚事务。 但是，资源管理器不能回滚事务后它被称为**ZwPrepareComplete**。

**提交阶段**

提交阶段 (也称为*第二阶段*) 的提交操作开始时 KTM 发送事务\_通知\_到所有资源管理器提交通知。 KTM 发送此通知后事务\_通知\_准备如果没有资源管理器支持单阶段提交或上级事务管理器会调用[ **ZwCommitEnlistment**](https://msdn.microsoft.com/library/windows/hardware/ff566419).

当每个资源管理器接收的事务\_通知\_提交通知时，它必须执行以下操作：

1.  永久和公共进行所有数据更改 (即，对其他事务可见)。

    通常情况下，资源管理器通过更改永久和公共中日志流事务的已保存的数据复制到数据库的公共、 永久存储。 有关如何使用日志流的详细信息，请参阅[使用日志流与 KTM 一起](using-log-streams-with-ktm.md)。

2.  调用[ **ZwCommitComplete**](https://msdn.microsoft.com/library/windows/hardware/ff566418)。

资源管理器调用后**ZwCommitComplete**，则应调用[ **ZwClose** ](https://msdn.microsoft.com/library/windows/hardware/ff566417)关闭登记句柄。

如果资源管理器遇到错误，正在进行的事务\_通知\_提交通知时，它应自行关闭。 操作系统重新加载的资源管理器，资源管理器的下一次[恢复过程](handling-recovery-operations.md)应还原到了已知保持完好，发生错误之前的状态的事务。

 

 




