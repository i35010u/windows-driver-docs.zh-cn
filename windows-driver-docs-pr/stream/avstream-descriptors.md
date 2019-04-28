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
ms.openlocfilehash: 10cc2380f80be9c48f0fa2e8df28b500f8e59809
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352622"
---
# <a name="avstream-descriptors"></a>AVStream 描述符





AVStream 微型驱动程序自身描述和筛选器将其类型支持在调用嵌套的描述符结构，从而[ **KsInitializeDriver**](https://msdn.microsoft.com/library/windows/hardware/ff562683)。 每个关键组件-设备[筛选器工厂](https://msdn.microsoft.com/library/windows/hardware/ff536385)，并[pin 工厂](https://msdn.microsoft.com/library/windows/hardware/ff537747)-都有关联的描述符。

如中所示[AVStream 对象层次结构](avstream-object-hierarchy.md)，AVStream 微型驱动程序的最高级别描述符是设备描述符[ **KSDEVICE\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff561691).

设备描述符中 **} Filterdescriptor**成员将指向数组 KSFILTER\_描述符结构描述类型的筛选器可以创建此设备。 AVStream 客户端可以调用[ **KsCreateFilterFactory** ](https://msdn.microsoft.com/library/windows/hardware/ff561650)动态地添加筛选器工厂。

KSFILTER\_描述符指示多少 pin 类型筛选器支持、 在其下的筛选器进行注册，KS 类别和筛选器的拓扑。 在每个筛选器描述符，微型驱动程序提供一个指针指向的数组[ **KSPIN\_描述符\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)结构。 每个这些 pin 描述符描述此筛选器可以实例化的 pin 类型。 可以通过调用创建其他的 pin 工厂[ **KsFilterCreatePinFactory**](https://msdn.microsoft.com/library/windows/hardware/ff562529)。

通常情况下，AVStream 微型驱动程序设置中，其源并调用的静态描述符表布局[ **KsInitializeDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562683)执行设置工作。 有关初始化您的驱动程序的详细信息，请参阅[初始化 AVStream 微型驱动程序](initializing-an-avstream-minidriver.md)。

还有其他类型的描述符，例如节点描述符[ **KSNODE\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563473)，它描述了给定的拓扑节点。

共有三种主要的描述符类型的每个调度表。 请参阅[AVStream 调度表](avstream-dispatch-tables.md)。

 

 




