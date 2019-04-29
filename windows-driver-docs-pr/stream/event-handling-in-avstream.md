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
ms.openlocfilehash: 28b24165e8b33c07030d7b4c97b11ff9f6d87a50
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363549"
---
# <a name="event-handling-in-avstream"></a>AVStream 中的事件处理





AVStream 筛选器和插针描述属性、 事件和它们支持通过提供的方法[ **KSAUTOMATION\_表**](https://msdn.microsoft.com/library/windows/hardware/ff560990)结构**AutomationTable**的成员[ **KSFILTER\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff562553)结构或[ **KSPIN\_描述符\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)结构。 有关详细信息，请参阅[AVStream 描述符](avstream-descriptors.md)。

若要支持事件，AVStream 微型驱动程序提供了一系列[ **KSEVENT\_设置**](https://msdn.microsoft.com/library/windows/hardware/ff561867)自动化表中的结构。 每个 KSEVENT\_集结构中包含的数组[ **KSEVENT\_项**](https://msdn.microsoft.com/library/windows/hardware/ff561862)结构。 每个 KSEVENT\_项结构介绍了如何微型驱动程序支持特定的事件。

微型驱动程序可以通过提供自定义事件行为[ *AVStrMiniAddEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff554260)并[ *AVStrMiniRemoveEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff556361)中的处理程序KSEVENT\_项结构。

AVStream 收到事件启用请求，它将生成 KSEVENT\_条目结构。 如果已提供微型驱动程序*AVStrAddEvent*处理程序，则 AVStream 会将指针传递到 KSEVENT\_对的调用中的条目结构*AVStrAddEvent*。

如果未提供*AVStrAddEvent*处理程序，然后 AVStream 默认情况下将事件添加到对象列表。 将微型驱动程序不会收到[ **KSEVENT\_条目**](https://msdn.microsoft.com/library/windows/hardware/ff561853)指针。 将微型驱动程序可以通过调用触发的事件[ **KsFilterGenerateEvents** ](https://msdn.microsoft.com/library/windows/hardware/ff562541)或[ **KsPinGenerateEvents**](https://msdn.microsoft.com/library/windows/hardware/ff563500)。

 

 




