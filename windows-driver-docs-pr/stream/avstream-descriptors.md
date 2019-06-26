---
title: AVStream 描述符
description: AVStream 描述符
ms.assetid: fd436406-311b-4537-994d-fbd8d92d4673
keywords:
- AVStream 描述符 WDK
- 描述符 WDK AVStream
- 嵌套的描述符结构 WDK AVStream
- AVStream 对象层次结构 WDK
- WDK AVStream 对象
- 层次结构 WDK AVStream
- 静态描述符表 WDK AVStream
- KSFILTER_DESCRIPTOR
- 设备描述符 WDK AVStream
- 筛选器工厂 WDK AVStream
- 筛选器类型 WDK AVStream
- 将固定类型 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c38d6a0c6bea452a832b95e338afd555aa665c07
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386704"
---
# <a name="avstream-descriptors"></a>AVStream 描述符





AVStream 微型驱动程序自身描述和筛选器将其类型支持在调用嵌套的描述符结构，从而[ **KsInitializeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)。 每个关键组件-设备[筛选器工厂](https://docs.microsoft.com/windows-hardware/drivers/audio/filter-factories)，并[pin 工厂](https://docs.microsoft.com/windows-hardware/drivers/audio/pin-factories)-都有关联的描述符。

如中所示[AVStream 对象层次结构](avstream-object-hierarchy.md)，AVStream 微型驱动程序的最高级别描述符是设备描述符[ **KSDEVICE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice_descriptor).

设备描述符中 **} Filterdescriptor**成员将指向数组 KSFILTER\_描述符结构描述类型的筛选器可以创建此设备。 AVStream 客户端可以调用[ **KsCreateFilterFactory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatefilterfactory)动态地添加筛选器工厂。

KSFILTER\_描述符指示多少 pin 类型筛选器支持、 在其下的筛选器进行注册，KS 类别和筛选器的拓扑。 在每个筛选器描述符，微型驱动程序提供一个指针指向的数组[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构。 每个这些 pin 描述符描述此筛选器可以实例化的 pin 类型。 可以通过调用创建其他的 pin 工厂[ **KsFilterCreatePinFactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksfiltercreatepinfactory)。

通常情况下，AVStream 微型驱动程序设置中，其源并调用的静态描述符表布局[ **KsInitializeDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksinitializedriver)执行设置工作。 有关初始化您的驱动程序的详细信息，请参阅[初始化 AVStream 微型驱动程序](initializing-an-avstream-minidriver.md)。

还有其他类型的描述符，例如节点描述符[ **KSNODE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksnode_descriptor)，它描述了给定的拓扑节点。

共有三种主要的描述符类型的每个调度表。 请参阅[AVStream 调度表](avstream-dispatch-tables.md)。

 

 




