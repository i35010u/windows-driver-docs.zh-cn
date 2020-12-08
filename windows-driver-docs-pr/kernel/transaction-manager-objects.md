---
title: 事务管理器对象
description: 事务管理器对象
keywords:
- 日志流 WDK KTM，创建
- 虚拟时钟值 WDK KTM，在事务管理器对象中
- 内核事务管理器 WDK，事务管理器
- 事务管理器对象 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e514b9c474b955581d47ff18d2dc9f60ead4020
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814261"
---
# <a name="transaction-manager-objects"></a>事务管理器对象


*事务管理器对象* 的主要目的是创建和维护 KTM 用来记录有关事务的状态信息的 [公用日志文件系统](introduction-to-the-common-log-file-system.md) (CLFS) 日志流。

事务管理器对象还包含一个 [虚拟时钟值](using-virtual-clock-values.md) ，KTM 维护该虚拟时钟值并将其用于对象的日志流中的序列信息。

KTM 提供一组可供内核模式[TPS 组件](understanding-tps-components.md)调用的[事务管理器对象例程](/windows-hardware/drivers/ddi/index)。 KTM 还提供用户模式应用程序可以调用的一组类似的用户模式例程。 有关用户模式例程的详细信息，请参阅 Microsoft Windows SDK。

资源管理器调用 [**ZwCreateTransactionManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreatetransactionmanager)时，KTM 会创建事务管理器对象。 通常，TPS 中的每个资源管理器都将创建一个事务管理器对象。 但您也可以设计一个 TPS，其中有多个资源管理器共享一个事务管理器对象。

TPS 组件可以通过调用 [**ZwOpenTransactionManager**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopentransactionmanager)打开现有事务管理器对象的其他句柄。 例如，如果 TPS 具有多个共享单个事务管理器对象的资源管理器，则一个资源管理器将调用 **ZwCreateTransactionManager** ，然后将对象 GUID 传递到其他资源管理器，以便它们可以调用 **ZwOpenTransactionManager**。

资源管理器通过调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)关闭它们对事务管理器对象的句柄。

当最后一个句柄关闭并且 KTM 释放了对该对象的所有引用后，操作系统将删除该对象。

 

