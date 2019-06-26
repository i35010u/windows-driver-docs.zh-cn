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
ms.openlocfilehash: fbcaf79e53824e4300a852ecaf2b58789e291490
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384104"
---
# <a name="event-handling-in-avstream"></a>AVStream 中的事件处理





AVStream 筛选器和插针描述属性、 事件和它们支持通过提供的方法[ **KSAUTOMATION\_表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksautomation_table_)结构**AutomationTable**的成员[ **KSFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_descriptor)结构或[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构。 有关详细信息，请参阅[AVStream 描述符](avstream-descriptors.md)。

若要支持事件，AVStream 微型驱动程序提供了一系列[ **KSEVENT\_设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_set)自动化表中的结构。 每个 KSEVENT\_集结构中包含的数组[ **KSEVENT\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_item)结构。 每个 KSEVENT\_项结构介绍了如何微型驱动程序支持特定的事件。

微型驱动程序可以通过提供自定义事件行为[ *AVStrMiniAddEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksaddevent)并[ *AVStrMiniRemoveEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksremoveevent)中的处理程序KSEVENT\_项结构。

AVStream 收到事件启用请求，它将生成 KSEVENT\_条目结构。 如果已提供微型驱动程序*AVStrAddEvent*处理程序，则 AVStream 会将指针传递到 KSEVENT\_对的调用中的条目结构*AVStrAddEvent*。

如果未提供*AVStrAddEvent*处理程序，然后 AVStream 默认情况下将事件添加到对象列表。 将微型驱动程序不会收到[ **KSEVENT\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksevent_entry)指针。 将微型驱动程序可以通过调用触发的事件[ **KsFilterGenerateEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfiltergenerateevents)或[ **KsPinGenerateEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingenerateevents)。

 

 




