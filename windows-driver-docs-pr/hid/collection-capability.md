---
title: 集合功能
description: 集合功能
ms.assetid: 228fab4f-ff90-43c5-bc68-26b29e8a7dd6
keywords:
- 功能 WDK HID 集合
- 摘要功能 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 603aa3125927f2dd91e1d13e0aac59d754edab94
ms.sourcegitcommit: 9145bffd4cc3b990a9ebff43b588db6ef2001f5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89592357"
---
# <a name="collection-capability"></a>集合功能





集合的功能由其使用情况、报表、链接集合和控件定义。 若要获取集合功能的摘要，用户模式应用程序或内核模式驱动程序会调用 [**HidP \_ GetCaps**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getcaps) 以获取 [**HidP \_ cap**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps) 结构。 此结构包含有关集合的 [链接集合](link-collections.md)、 [按钮功能数组](button-capability-arrays.md)和 [值功能数组](value-capability-arrays.md)的下列信息：

-   集合的 " [使用](hid-usages.md#usage-page) 情况" 页和 [使用 ID](hid-usages.md#usage-id)

-   集合的输入、输出和功能报表的大小（以字节为单位） (参阅 [HID 概念简介](introduction-to-hid-concepts.md)) 

-   集合的[链接集合](link-collections.md#ddk-link-collection-array-kg)中的[**HIDP \_ 链接 \_ 集合 \_ 节点**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_link_collection_node)结构数

-   对于每个报表类型，由[**HIDP \_ GetButtonCaps**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getbuttoncaps)返回的 button 功能数组中[**HIDP \_ 按钮 \_ 帽**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_button_caps)结构的数目

-   对于每个报表类型，为[**HIDP \_ GetValueCaps**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getvaluecaps)返回的 value 功能数组中[**HIDP \_ 值的 \_ 上限**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_value_caps)结构的数目

-   对于每个报表类型，为集合支持的按钮和值的数目，由 **Number***Xxx***DataIndices** 成员指定。

 

