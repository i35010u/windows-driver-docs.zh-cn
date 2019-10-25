---
title: 属性上下文
description: 属性上下文
ms.assetid: da33848c-a9bc-40c7-ab1b-0ca056f3e06d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61cc8517f4c9131e29b7486fa6a23cb8dca4557e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840773"
---
# <a name="property-contexts"></a>属性上下文





属性上下文为微型驱动程序提供了一种方便的方法，以便在验证这些属性的过程中标识它感兴趣的多个属性。 使用属性上下文，微型驱动程序可以快速确定是否更改了任何标识的属性。 然后，微型驱动程序将属性上下文传递给 WIA 服务库函数之一（例如， [**wiasGetChangedValueFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)），后者使用上下文来确定应用程序是否在更改属性的值。

验证的 WIA 方法是在应用程序更改属性时，还应更新所有依赖属性。 但是，如果应用程序也更改了依赖属性，只需检查顶级属性以确定其新值是否有效。 与属性验证相关的 WIA 服务库函数使用此原则来决定何时应更新依赖属性以及何时应检查有效性。

在[**WIA\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_property_context)中维护一组属性的上下文\_上下文结构，其中包含三个成员：属性上下文中的属性数目、指向属性标识符（PROPIDs）的数组的指针和指向的指针。布尔值的数组。 将并行维护数组（即属性标识符数组中索引为*N*的属性与布尔值数组中位于同一索引处的布尔值相关联）。

微型驱动程序调用 WIA 服务库函数[**wiasCreatePropContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatepropcontext)来分配内存并填充属性上下文的值。 其他 WIA 服务库函数（如[**wiasGetChangedValueFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)）使用属性上下文来确定何时应更新属性的值。

 

 




