---
title: 集合功能
description: 集合功能
ms.assetid: 228fab4f-ff90-43c5-bc68-26b29e8a7dd6
keywords:
- 功能 WDK HID 集合
- WDK HID 的功能摘要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54f6fb798b3c8647edba1bf7192814627acd3360
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554189"
---
# <a name="collection-capability"></a>集合功能





由其使用情况、 报表、 链接集合和控件定义的集合的功能。 若要获取的集合的功能摘要，用户模式应用程序或内核模式驱动程序调用[ **HidP\_GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff539715)若要获取[ **HIDP\_CAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff539697)结构。 此结构包含有关集合的以下信息[将集合链接](link-collections.md)，[按钮功能数组](button-capability-arrays.md)，并[值功能数组](value-capability-arrays.md):

-   集合的[使用情况页面](hid-usages.md#usage-page)和[用法 ID](hid-usages.md#usage-id)

-   大小 （字节） 集合的输入、 输出和报告功能 (请参阅[HID 概念简介](introduction-to-hid-concepts.md))

-   数[ **HIDP\_链接\_集合\_节点**](https://msdn.microsoft.com/library/windows/hardware/ff539764)集合中的结构[链接集合数组](link-collections.md#ddk-link-collection-array-kg)

-   对于每个报表类型，数[ **HIDP\_按钮\_CAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff539693)按钮功能阵列中的结构返回[ **HidP\_GetButtonCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539707)

-   对于每个报表类型，数[ **HIDP\_值\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/ff539832)值功能数组中的结构返回[ **HidP\_GetValueCaps**](https://msdn.microsoft.com/library/windows/hardware/ff539754)

-   每种报告类型、 按钮和支持的集合，指定的值的数量**数量***Xxx***DataIndices**成员。

 

 




