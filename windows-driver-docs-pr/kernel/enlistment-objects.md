---
title: 登记对象
description: 登记对象
keywords:
- 登记 WDK KTM
- 登记 WDK KTM，对象
- 资源管理器 WDK KTM，创建登记
- 内核事务管理器 WDK，登记
- KTM WDK，登记
- 登记对象 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: be329dc1bbee63f7ed40c89091a600ecf1152377
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824017"
---
# <a name="enlistment-objects"></a>登记对象


*征用对象* 表示资源管理器在事务中的 [*登记*](transaction-processing-terms.md#ktm-term-enlistment)。 在资源管理器可以接收有关事务事件的通知之前，资源管理器必须调用 [**ZwCreateEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntcreateenlistment) 来创建对事务的登记。

KTM 提供一组可供内核模式资源管理器调用的 [登记对象例程](/windows-hardware/drivers/ddi/index) 。 KTM 还提供用户模式应用程序可以调用的一组类似的用户模式例程。 有关用户模式例程的详细信息，请参阅 Microsoft Windows SDK。

当资源管理器调用 **ZwCreateEnlistment** ，以便在资源管理器从事务客户端) 中接收 (时，KTM 会创建登记对象。

[TPS 组件](understanding-tps-components.md) 可以调用 [**ZwOpenEnlistment**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntopenenlistment) 来打开登记对象的其他句柄。 但大多数 TPS 设计不需要额外的开放句柄。

资源管理器通过调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)将其句柄关闭到登记对象。 如果在提交关联的事务对象之前，最后一个句柄已关闭，则 KTM 会将事务 \_ 通知 \_ 回滚通知发送到所有具有事务登记的资源管理器。

当最后一个句柄关闭并且 KTM 释放了对该对象的所有引用后，操作系统将删除该对象。

 

