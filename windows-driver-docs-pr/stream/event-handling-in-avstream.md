---
title: AVStream 中的事件处理
description: AVStream 中的事件处理
keywords:
- 事件 WDK AVStream
- AVStream 事件 WDK
- 自动化表 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef7c5968f7470a8dc831eb29e4f2cdeee7233a9d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837623"
---
# <a name="event-handling-in-avstream"></a>AVStream 中的事件处理





AVStream 筛选器和 pin 介绍了其支持的属性、事件和方法，这些属性、事件和方法通过在 [**KSFILTER \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)结构或 [**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构的 **AutomationTable** 成员中提供 [**KSAUTOMATION \_ 表**](/windows-hardware/drivers/ddi/ks/ns-ks-ksautomation_table_)结构来提供支持。 有关详细信息，请参阅 [AVStream 描述符](avstream-descriptors.md)。

为了支持事件，AVStream 微型驱动程序在自动化表中提供了一个 [**KSEVENT \_ 集**](/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_set) 结构的数组。 每个 KSEVENT \_ 集结构都包含 [**KSEVENT \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_item) 结构的数组。 每个 KSEVENT \_ 项结构都说明了微型驱动程序如何支持特定事件。

微型驱动程序可以通过在 KSEVENT 项结构中提供 [*AVStrMiniAddEvent*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksaddevent) 和 [*AVStrMiniRemoveEvent*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksremoveevent) 处理程序来自定义事件行为 \_ 。

当 AVStream 收到事件 enable 请求时，它将生成 KSEVENT \_ 条目结构。 如果微型驱动程序提供了 *AVStrAddEvent* 处理程序，AVStream \_ 将在对 *AVStrAddEvent* 的调用中传递一个指向 KSEVENT 条目结构的指针。

如果未提供 *AVStrAddEvent* 处理程序，则默认情况下 AVStream 会将事件添加到对象列表中。 你的微型驱动程序不会接收 [**KSEVENT \_ 条目**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksevent_entry) 指针。 微型驱动程序可以通过调用 [**KsFilterGenerateEvents**](/windows-hardware/drivers/ddi/ks/nf-ks-ksfiltergenerateevents) 或 [**KsPinGenerateEvents**](/windows-hardware/drivers/ddi/ks/nf-ks-kspingenerateevents)触发事件。

 

