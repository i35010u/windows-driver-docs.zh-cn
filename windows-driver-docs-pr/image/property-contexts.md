---
title: 属性上下文
description: 属性上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd536cf648298700999f316fcb4675132a28f31b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831401"
---
# <a name="property-contexts"></a>属性上下文





属性上下文为微型驱动程序提供了一种方便的方法，以便在验证这些属性的过程中标识它感兴趣的多个属性。 使用属性上下文，微型驱动程序可以快速确定是否更改了任何标识的属性。 然后，微型驱动程序将属性上下文传递给某个 WIA 服务库函数 (例如， [**wiasGetChangedValueFloat**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)) ，后者使用上下文来确定应用程序是否在更改属性的值。

验证的 WIA 方法是在应用程序更改属性时，还应更新所有依赖属性。 但是，如果应用程序也更改了依赖属性，只需检查顶级属性以确定其新值是否有效。 与属性验证相关的 WIA 服务库函数使用此原则来决定何时应更新依赖属性以及何时应检查有效性。

在 [**WIA \_ 属性 \_ 上下文**](/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_context) 结构中维护一组属性的上下文，其中包含三个成员：属性上下文中的属性数目、指向属性标识符数组的指针 (PROPIDs) ，以及一个指向布尔值数组的指针。 数组是并行维护的 (也就是说，属性标识符位于属性标识符数组中的索引 *N* 处的属性与 bool 数组中同一索引处的 bool 值相关联) 。

微型驱动程序调用 WIA 服务库函数 [**wiasCreatePropContext**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)来分配内存并填充属性上下文的值。 其他 WIA 服务库函数（如 [**wiasGetChangedValueFloat**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)）使用属性上下文来确定何时应更新属性的值。

 

