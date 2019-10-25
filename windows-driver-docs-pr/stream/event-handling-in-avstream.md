---
title: AVStream 中的事件处理
description: AVStream 中的事件处理
ms.assetid: 7add2055-8d3f-432d-8aa1-44459ac197dd
keywords:
- 事件 WDK AVStream
- AVStream 事件 WDK
- 自动化表 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ea9dd5581d657bd38a0b274c51c01296d2f1bfc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826209"
---
# <a name="event-handling-in-avstream"></a>AVStream 中的事件处理





AVStream 筛选器和 pin 说明了其支持的属性、事件和方法，这些属性、事件和方法通过在[**KSFILTER\_说明符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)结构的**AutomationTable**成员中提供[**KSAUTOMATION\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksautomation_table_)结构或[**KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构。 有关详细信息，请参阅[AVStream 描述符](avstream-descriptors.md)。

为支持事件，AVStream 微型驱动程序提供了一个 KSEVENT 表中的[ **\_集**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_set)结构的数组。 每个 KSEVENT\_集结构包含一组[**KSEVENT\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_item)结构。 每个 KSEVENT\_项结构都说明了微型驱动程序如何支持特定事件。

微型驱动程序可以通过在 KSEVENT\_项结构中提供[*AVStrMiniAddEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksaddevent)和[*AVStrMiniRemoveEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksremoveevent)处理程序来自定义事件行为。

当 AVStream 收到事件 enable 请求时，它会生成一个 KSEVENT\_条目结构。 如果微型驱动程序提供了*AVStrAddEvent*处理程序，AVStream 将在调用*AVSTRADDEVENT*时向 KSEVENT\_条目结构传递一个指针。

如果未提供*AVStrAddEvent*处理程序，则默认情况下 AVStream 会将事件添加到对象列表中。 你的微型驱动程序不会接收[**KSEVENT\_入口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksevent_entry)指针。 微型驱动程序可以通过调用[**KsFilterGenerateEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfiltergenerateevents)或[**KsPinGenerateEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingenerateevents)触发事件。

 

 




