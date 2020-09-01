---
title: AVStream 中的流控制门
description: AVStream 中的流控制门
ms.assetid: c5592f92-a432-44e3-afe0-60fcf917a443
keywords:
- AVStream 逻辑关口 WDK
- 逻辑门 WDK AVStream
- 关口 WDK AVStream
- 和关口 WDK AVStream
- KSGATE
- 流控制入口 WDK AVStream
- 处理控制入口 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f436129ad01c176d4f714c829f275e195e926289
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191437"
---
# <a name="flow-control-gates-in-avstream"></a>AVStream 中的流控制门





AVStream 使用逻辑入口作为控制流机制。 每个逻辑门由一个 [**KSGATE**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksgate) 结构表示。

AVStream 使用单和门初始化每个筛选器或 pin。 然后，微型驱动程序可以使用此机制来确定特定对象处理数据的时间。 若要检索 pin 的处理控制门，微型驱动程序调用 [**KsPinGetAndGate**](/windows-hardware/drivers/ddi/ks/nf-ks-kspingetandgate)。 若要检索筛选器的处理控制门，请调用 [**KsFilterGetAndGate**](/windows-hardware/drivers/ddi/ks/nf-ks-ksfiltergetandgate)。

若要创建新的逻辑入口，微型驱动程序调用 [**KsGateInitializeAnd**](/windows-hardware/drivers/ddi/ks/nf-ks-ksgateinitializeand) 或 [**KsGateInitializeOr**](/windows-hardware/drivers/ddi/ks/nf-ks-ksgateinitializeor)。 可以使用一个入口的输出作为另一个入口的输入，从而转发状态转换。 为此，请在这些调用中提供 *NextOrGate* 或 *NextAndGate* 参数。

若要关闭逻辑入口的现有输入，可以调用 [**KsGateTurnInputOff**](/windows-hardware/drivers/ddi/ks/nf-ks-ksgateturninputoff)。 微型驱动程序可能会导致此调用停止和关闭活动的 pin，或在无限期内暂停处理。

同样，可以调用 [**KsGateTurnInputOn**](/windows-hardware/drivers/ddi/ks/nf-ks-ksgateturninputon) 来打开现有的特定入口输入。

当线程准备好进行处理时，它会尝试捕获控制处理对象处理的和*入口的。* 为此，微型驱动程序调用了 [**KsGateCaptureThreshold**](/windows-hardware/drivers/ddi/ks/nf-ks-ksgatecapturethreshold)。

如果和入口为打开状态，则 AVStream 会关闭入口的输入，并且处理开始。 由于入口在处理过程中已关闭，因此没有其他线程可以捕获入口*的输入。* 一次只能有一个线程可以处理数据。

若要在不进行修改的情况下检查入口的状态，微型驱动程序可以调用 [**KsGateGetStateUnsafe**](/windows-hardware/drivers/ddi/ks/nf-ks-ksgategetstateunsafe)。 但请注意，此函数不会处理同步。

若要删除逻辑入口，请调用 [**KsGateTerminateAnd**](/windows-hardware/drivers/ddi/ks/nf-ks-ksgateterminateand) 或 [**KsGateTerminateOr**](/windows-hardware/drivers/ddi/ks/nf-ks-ksgateterminateor)。 要删除的入口必须位于入口链的开头。

若要将 pin 作为输入附加到逻辑入口，然后将相同的逻辑入口连接到筛选器和入口的输入，请调用 [**KsPinAttachAndGate**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinattachandgate) 或 [**KsPinAttachOrGate**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinattachorgate)。

### <a name="determining-gate-status"></a>确定入口状态

对于和入口，KSGATE 结构的 **Count** 成员的值为 *减去输入数量* 减一：

Count = 1- (*关* 输入数量) 

如果此值小于或等于零，则入口被关闭。 如果此值大于零，则门处于打开状态。

对于或入口，KSGATE 的 **Count** 成员的值 *是输入到入口的数目* ：

计数 = * (输入数量*) 

如果此值等于零，则关闭入口。 如果 **Count** 大于零，则门处于打开状态。

和入口的 **计数** 范围为1或更小;或入口的有效 **计数** 范围为零或更大。 不要将 **计数** 设置为无效值; *AVStream 不会验证微型驱动程序是否已将入口设置为有效状态。*

 

