---
title: 集合功能
description: 集合功能
ms.assetid: 228fab4f-ff90-43c5-bc68-26b29e8a7dd6
keywords:
- 功能 WDK HID 集合
- WDK HID 的功能摘要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49a396ebe313943520269c8f2c507659b99b7deb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375767"
---
# <a name="collection-capability"></a>集合功能





由其使用情况、 报表、 链接集合和控件定义的集合的功能。 若要获取的集合的功能摘要，用户模式应用程序或内核模式驱动程序调用[ **HidP\_GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getcaps)若要获取[ **HIDP\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_caps)结构。 此结构包含有关集合的以下信息[将集合链接](link-collections.md)，[按钮功能数组](button-capability-arrays.md)，并[值功能数组](value-capability-arrays.md):

-   集合的[使用情况页面](hid-usages.md#usage-page)和[用法 ID](hid-usages.md#usage-id)

-   大小 （字节） 集合的输入、 输出和报告功能 (请参阅[HID 概念简介](introduction-to-hid-concepts.md))

-   数[ **HIDP\_链接\_集合\_节点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_link_collection_node)集合中的结构[链接集合数组](link-collections.md#ddk-link-collection-array-kg)

-   对于每个报表类型，数[ **HIDP\_按钮\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_button_caps)按钮功能阵列中的结构返回[ **HidP\_GetButtonCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getbuttoncaps)

-   对于每个报表类型，数[ **HIDP\_值\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_value_caps)值功能数组中的结构返回[ **HidP\_GetValueCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getvaluecaps)

-   每种报告类型、 按钮和支持的集合，指定的值的数量**数量***Xxx***DataIndices**成员。

 

 




