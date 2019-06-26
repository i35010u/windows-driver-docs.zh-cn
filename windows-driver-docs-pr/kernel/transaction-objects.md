---
title: 事务对象
description: 事务对象
ms.assetid: 124105bd-70be-49b1-8ea4-af6ba1f3cf16
keywords:
- 事务 WDK KTM，对象
- WDK KTM 的事务
- 事务客户端 WDK KTM，创建事务
- 内核事务管理器 WDK 事务
- KTM WDK 事务
- WDK KTM 的事务对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb0a41d448e01bb13d5fe6dae95ed0d661605e3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382942"
---
# <a name="transaction-objects"></a>事务对象


*事务对象*表示事务。 事务的客户端创建一个事务、 执行一些工作，并提交或回滚事务。

KTM 提供了一套[事务对象例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)内核模式下事务客户端可以调用。 KTM 还提供了一组类似的用户模式下用户模式应用程序可以调用的例程。 有关用户模式下例程的详细信息，请参阅 Microsoft Windows SDK。

KTM 创建事务对象时在客户端调用[ **ZwCreateTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcreatetransaction)。 客户端可以调用[ **ZwCommitTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntcommittransaction)或[ **ZwRollbackTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntrollbacktransaction)来提交或回滚事务。

[TP 组件](understanding-tps-components.md)可以调用[ **ZwOpenTransaction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntopentransaction)打开附加到事务对象的句柄。

客户端通过调用关闭其对事务对象的句柄[ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)。 如果之前已提交的事务对象，最后一个句柄已关闭，KTM 发送事务\_通知\_回滚通知到具有该事务的登记的所有资源管理器。

在最后一个句柄已关闭并且 KTM 已释放其对该对象的所有引用之后，操作系统将删除对象。

 

 




