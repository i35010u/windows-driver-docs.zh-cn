---
title: AVStream 中的流控制门
description: AVStream 中的流控制门
ms.assetid: c5592f92-a432-44e3-afe0-60fcf917a443
keywords:
- AVStream 逻辑门 WDK
- 逻辑门 WDK AVStream
- 入口 WDK AVStream
- 和入口 WDK AVStream
- KSGATE
- 流控制门 WDK AVStream
- 处理控件门 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00a077e26860ef579a0e39d7b7188f0bd7ed83dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376109"
---
# <a name="flow-control-gates-in-avstream"></a>AVStream 中的流控制门





AVStream 使用控制流机制作为逻辑门。 表示每个逻辑门[ **KSGATE** ](https://msdn.microsoft.com/library/windows/hardware/ff562566)结构。

AVStream 初始化每个筛选器或使用单个 AND 关卡的 pin。 然后，微型驱动程序可以使用此机制来确定该特定对象时可以处理数据。 若要检索的 pin 处理控制门，微型驱动程序调用[ **KsPinGetAndGate**](https://msdn.microsoft.com/library/windows/hardware/ff563502)。 若要检索筛选器处理控制门，调用[ **KsFilterGetAndGate**](https://msdn.microsoft.com/library/windows/hardware/ff562542)。

若要创建新的逻辑门，微型驱动程序调用[ **KsGateInitializeAnd** ](https://msdn.microsoft.com/library/windows/hardware/ff562574)或[ **KsGateInitializeOr**](https://msdn.microsoft.com/library/windows/hardware/ff562576)。 您可以使用一个关口输出输入到另一个入口，从而转发状态转换。 若要执行此操作，提供*NextOrGate*或*NextAndGate*中这些调用的参数。

若要关闭的逻辑入口的现有输入，可以调用[ **KsGateTurnInputOff**](https://msdn.microsoft.com/library/windows/hardware/ff562589)。 微型驱动程序可能会进行此调用，以停止并关闭活动的 pin，或若要挂起处理无限期的时间。

同样，调用[ **KsGateTurnInputOn** ](https://msdn.microsoft.com/library/windows/hardware/ff562591)以打开特定的门限的现有输入。

当一个线程已准备好处理时，它会尝试捕获*上*和网关，以控制处理对象的处理的输入。 若要执行此操作，微型驱动程序调用[ **KsGateCaptureThreshold**](https://msdn.microsoft.com/library/windows/hardware/ff562571)。

如果 AND 门处于打开状态，AVStream 将关闭门限的输入，并开始处理。 由于在处理过程现在关闭门，没有其他线程可以捕获*上*输入的门。 只有一个线程可以一次处理数据。

若要检查的入口状态而无需修改它，微型驱动程序可以调用[ **KsGateGetStateUnsafe**](https://msdn.microsoft.com/library/windows/hardware/ff562572)。 但请注意，此函数不会处理同步。

若要删除的逻辑入口，调用[ **KsGateTerminateAnd** ](https://msdn.microsoft.com/library/windows/hardware/ff562586)或[ **KsGateTerminateOr**](https://msdn.microsoft.com/library/windows/hardware/ff562588)。 入口链的开头必须是要删除的入口。

若要将 pin 附加为逻辑门限的输入，然后连接作为筛选器的输入相同的逻辑入口和入口，请调用[ **KsPinAttachAndGate** ](https://msdn.microsoft.com/library/windows/hardware/ff563491)或[ **KsPinAttachOrGate**](https://msdn.microsoft.com/library/windows/hardware/ff563492).

### <a name="determining-gate-status"></a>确定入口状态

为 AND 入口的值**计数**KSGATE 结构中的成员是 1 的数减去*关闭*输入：

Count = 1-(数*关闭*输入)

如果此值小于或等于零，门已关闭。 如果此值大于零，门处于打开状态。

为或入口的值**计数**KSGATE 成员是数*上*门的输入：

计数 = (数*上*输入)

如果此值等于零，则关闭门。 如果**计数**是大于零，门处于打开状态。

和入口具有有效**计数**范围的一个或更少;或入口具有有效**计数**范围的零个或更高版本。 未设置**计数**为无效值;*AVStream 不会验证微型驱动程序已设置为有效状态的门。*

 

 




