---
title: KTM 对象
description: KTM 对象
keywords:
- 内核事务管理器 WDK，对象
- KTM WDK，对象
- 对象 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: db3368375752a32bb606719dbe288ae972de2240
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801671"
---
# <a name="ktm-objects"></a>KTM 对象


内核事务管理器 (KTM) 定义以下四种对象类型：

-   [事务管理器对象](transaction-manager-objects.md)，KTM 使用该对象维护有关 [*事务处理系统*](transaction-processing-terms.md#ktm-term-transaction-processing-system) (TPS) 的 [*日志流*](transaction-processing-terms.md#ktm-term-log-stream)的内存驻留信息。

-   [资源管理器对象](resource-manager-objects.md)，表示 TPS 内的 [*资源管理*](transaction-processing-terms.md#ktm-term-resource-manager) 器。

-   [事务对象](transaction-objects.md)，表示 [*事务性客户端*](transaction-processing-terms.md#ktm-term-transactional-client) 创建的事务。

-   [登记对象](enlistment-objects.md)，这些对象表示提供事务和资源管理器之间的连接的 [*登记*](transaction-processing-terms.md#ktm-term-enlistment) 。

这四种对象类型都具有以下特征：

-   若要创建对象并获取对象句柄， [TPS 组件](understanding-tps-components.md) 可以调用 *创建* 例程。

-   为了获取现有对象的其他对象句柄，TPS 组件可以调用 *打开* 的例程。

-   若要获取有关对象的信息，TPS 组件可以调用 *查询* 例程。

-   为了关闭对象句柄，TPS 组件调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)。

KTM 将标识符 GUID 分配给每个对象。 对于事务对象，此标识符 GUID 也称为客户端可以指定的 *工作单元 (UOW) 标识符* 。 TPS 组件可使用标识符 Guid 跟踪对象。 创建对象的 TPS 组件可以将对象的标识符 GUID 传递到另一个组件，使后一组件可以打开对象的句柄。

使用 KTM 的任何 TPS 组件都可以调用 [**ZwEnumerateTransactionObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ntenumeratetransactionobject) 来枚举 KTM 对象，但大多数组件不需要调用此例程。

本节包含下列主题：

[事务管理器对象](transaction-manager-objects.md)

[资源管理器对象](resource-manager-objects.md)

[事务对象](transaction-objects.md)

[登记对象](enlistment-objects.md)

 

