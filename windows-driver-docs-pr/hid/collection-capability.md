---
title: 集合功能
description: 集合功能
ms.assetid: 228fab4f-ff90-43c5-bc68-26b29e8a7dd6
keywords:
- 功能 WDK HID 集合
- 摘要功能 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 477888c224dca2ca8f075d6e649b1bd0d069c89d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824843"
---
# <a name="collection-capability"></a>集合功能





集合的功能由其使用情况、报表、链接集合和控件定义。 若要获取集合功能的摘要，用户模式应用程序或内核模式驱动程序调用[**HidP\_GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getcaps)以获取[**HidP\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)结构。 此结构包含有关集合的[链接集合](link-collections.md)、[按钮功能数组](button-capability-arrays.md)和[值功能数组](value-capability-arrays.md)的下列信息：

-   集合的 "[使用](hid-usages.md#usage-page)情况" 页和[使用 ID](hid-usages.md#usage-id)

-   集合的输入、输出和功能报表的大小（以字节为单位）（请参阅[HID 概念简介](introduction-to-hid-concepts.md)）

-   集合的[链接集合数组](link-collections.md#ddk-link-collection-array-kg)中[ **\_节点结构的 HIDP\_链接\_集合**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_link_collection_node)

-   对于每个报表类型，由[**HIDP\_GetButtonCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getbuttoncaps)返回的按钮功能数组中的[**HIDP\_"按钮的数目\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_button_caps)结构

-   对于每个报表类型， [**HIDP\_GetValueCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getvaluecaps)返回的 value 功能数组中的[**HIDP\_值\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_value_caps)结构的数目

-   对于每个报表类型，为集合支持的按钮和值的数目，由**Number***Xxx***DataIndices**成员指定。

 

 




