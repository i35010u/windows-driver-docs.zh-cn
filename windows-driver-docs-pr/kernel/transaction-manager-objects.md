---
title: 事务管理器对象
description: 事务管理器对象
ms.assetid: af53cda4-e2ab-47df-9311-a4da2a2ee08d
keywords:
- 日志流 WDK KTM，创建
- 虚拟时钟值 WDK KTM 事务管理器对象中
- 内核事务管理器 WDK，事务管理器
- 事务管理器对象 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f617d8724a5e38a389f54510802ba5084b7955c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385493"
---
# <a name="transaction-manager-objects"></a>事务管理器对象


主要目的*事务管理器对象*是创建和维护[公用日志文件系统](using-common-log-file-system.md)KTM 使用记录状态有关的信息的事务 (CLFS) 日志流。

事务管理器对象还包含[虚拟时钟值](using-virtual-clock-values.md)KTM 维护，并使用序列对象的日志流中的信息。

KTM 提供了一套[事务管理器对象例程](https://msdn.microsoft.com/library/windows/hardware/ff564807)内核模式[TP 组件](understanding-tps-components.md)可以调用。 KTM 还提供了一组类似的用户模式下用户模式应用程序可以调用的例程。 有关用户模式下例程的详细信息，请参阅 Microsoft Windows SDK。

KTM 创建事务管理器对象，当资源管理器调用[ **ZwCreateTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff566430)。 通常情况下，在 TP 中的每个资源管理器创建一个事务管理器对象。 但您还可以设计多个资源管理器在其中共享单个事务管理器对象 TPS。

TP 组件可以通过调用打开附加到现有的事务管理器对象的句柄[ **ZwOpenTransactionManager**](https://msdn.microsoft.com/library/windows/hardware/ff567035)。 例如，如果你 TP 具有共享的单个事务管理器对象的多个资源管理器，一个资源管理器将调用**ZwCreateTransactionManager**然后将对象的 GUID 传递给其他资源管理器，以便它们可以调用**ZwOpenTransactionManager**。

资源管理器关闭其对象的句柄事务管理器通过调用[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)。

在最后一个句柄已关闭并且 KTM 已释放其对该对象的所有引用之后，操作系统将删除对象。

 

 




