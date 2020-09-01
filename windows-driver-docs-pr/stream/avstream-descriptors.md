---
title: AVStream 描述符
description: AVStream 描述符
ms.assetid: fd436406-311b-4537-994d-fbd8d92d4673
keywords:
- AVStream 描述符 WDK
- 描述符 WDK AVStream
- 嵌套描述符结构 WDK AVStream
- AVStream 对象层次结构 WDK
- 对象 WDK AVStream
- 层次结构 WDK AVStream
- 静态描述符表 WDK AVStream
- KSFILTER_DESCRIPTOR
- 设备描述符 WDK AVStream
- 筛选工厂 WDK AVStream
- 筛选器类型 WDK AVStream
- pin 类型 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a36f01388312fc1f3a3c7bc66034eeac45d76a0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192421"
---
# <a name="avstream-descriptors"></a>AVStream 描述符





AVStream 微型驱动程序通过在对 [**KsInitializeDriver**](/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver)的调用中提供嵌套的描述符结构来描述自身及其支持的筛选器类型。 每个关键组件（设备、 [筛选器工厂](../audio/filter-factories.md)和 [pin 工厂](../audio/pin-factories.md) ）都有一个关联的描述符。

如 [AVStream 对象层次结构](avstream-object-hierarchy.md)中所示，AVStream 微型驱动程序的最高级别描述符是设备描述符， [**KSDEVICE \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_descriptor)。

在设备描述符中， **filterdescriptor** 成员指向 \_ 描述此设备可以创建的筛选器类型的 KSFILTER 描述符结构的数组。 AVStream 客户端可以调用 [**KsCreateFilterFactory**](/windows-hardware/drivers/ddi/ks/nf-ks-kscreatefilterfactory) 来动态添加筛选器工厂。

KSFILTER \_ 描述符指示筛选器支持的 pin 类型数、用于注册筛选器的 KS 类别以及筛选器的拓扑。 在每个筛选器描述符中，微型驱动程序提供指向 [**KSPIN \_ 说明符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex) 结构的数组的指针。 其中每个 pin 说明符描述此筛选器可以实例化的 pin 类型。 可以通过调用 [**KsFilterCreatePinFactory**](/windows-hardware/drivers/ddi/ks/nf-ks-ksfiltercreatepinfactory)来创建其他 pin 工厂。

通常情况下，AVStream 微型驱动程序会在其源中布局静态描述符表，并调用 [**KsInitializeDriver**](/windows-hardware/drivers/ddi/ks/nf-ks-ksinitializedriver) 来执行设置工作。 有关初始化驱动程序的详细信息，请参阅 [初始化 AVStream 微型驱动程序](initializing-an-avstream-minidriver.md)。

还存在其他类型的描述符，如用于描述给定拓扑节点的节点描述符 [**KSNODE \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksnode_descriptor)。

调度表对于这三种主要描述符类型中的每一种都是通用的。 请参阅 [AVStream 调度表](avstream-dispatch-tables.md)。

 

