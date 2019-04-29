---
title: KTM 对象
description: KTM 对象
ms.assetid: 927a417b-35f5-49b8-85f3-7e6b1f5c0225
keywords:
- 内核事务管理器 WDK 对象
- KTM WDK 对象
- WDK KTM 对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 153a1e71943b3ef96f0be3e4636554d003dec5b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381379"
---
# <a name="ktm-objects"></a>KTM 对象


内核事务管理器 (KTM) 定义了以下四个对象类型：

-   [事务管理器对象](transaction-manager-objects.md)，用于维护有关驻留在内存中的信息 KTM [*日志流*](transaction-processing-terms.md#ktm-term-log-stream)有关[*事务处理系统* ](transaction-processing-terms.md#ktm-term-transaction-processing-system) (TPS)。

-   [资源管理器对象](resource-manager-objects.md)，表示[*资源管理器*](transaction-processing-terms.md#ktm-term-resource-manager) TP 内。

-   [事务对象](transaction-objects.md)，这表示事务的[*事务的客户端*](transaction-processing-terms.md#ktm-term-transactional-client)创建。

-   [登记对象](enlistment-objects.md)，表示[*登记*](transaction-processing-terms.md#ktm-term-enlistment)提供事务和资源管理器之间的连接。

所有这些四个对象类型具有以下特征：

-   若要创建一个对象，并获取对象句柄， [TP 组件](understanding-tps-components.md)可以调用*创建*例程。

-   若要获取对现有对象的其他对象句柄，TP 组件可以调用*打开*例程。

-   若要获取的对象有关的信息，请 TP 组件可以调用*查询*例程。

-   若要关闭对象句柄，TP 组件调用[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)。

KTM 将标识符 GUID 分配给每个对象。 对于事务对象，此标识符 GUID 是也称为*单元的工作 (UOW) 标识符*，可以指定客户端。 TP 组件可以使用标识符 Guid 跟踪对象。 TP 组件用于创建对象可以将对象的标识符的 GUID 传递给另一个组件，以便后一种组件可以打开对象的句柄。

可以调用任何 TP 组件，它使用 KTM [ **ZwEnumerateTransactionObject** ](https://msdn.microsoft.com/library/windows/hardware/ff566450)枚举 KTM 对象，但大多数组件无需调用该例程。

本部分包含以下主题：

[事务管理器对象](transaction-manager-objects.md)

[资源管理器对象](resource-manager-objects.md)

[事务对象](transaction-objects.md)

[登记的对象](enlistment-objects.md)

 

 




