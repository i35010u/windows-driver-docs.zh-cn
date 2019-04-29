---
title: 帧注入
description: 帧注入
ms.assetid: cdfb1763-92a8-4a60-8f49-2af34a8beca5
keywords:
- 帧 WDK AVStream
- 注入模式 WDK AVStream 帧
- 帧注入 WDK AVStream
- pin 为中心的筛选器 WDK AVStream
- 筛选器为中心的筛选器 WDK AVStream
- 空帧 WDK AVStream
- 默认框架行为 WDK AVStream
- 重写默认框架行为 WDK 流式处理媒体
- 线路 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ef84ec774a23a05762718d3bbbe16e58ab7833a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376123"
---
# <a name="frame-injection"></a>帧注入





默认情况下，在 AVStream 请求者获取中分配器的空帧，并将它们放在队列中。 微型驱动程序然后填充帧通过[pin 以中心处理](pin-centric-processing.md)或[筛选器以中心处理](filter-centric-processing.md)。 跨传输将移动帧到线路，最终完成线路并返回给请求者中的下一个对象。 AVStream 然后重用帧。

微型驱动程序可以通过使用替代此默认行为*注入模式*。 在注入模式下，微型驱动程序负责将框架放入该线路。 帧周围以默认方式线路传播。 微型驱动程序提供当帧回到 AVStream 对象的开始位置时，请调用 AVStream [ *AVStrMiniFrameReturn* ](https://msdn.microsoft.com/library/windows/hardware/ff556320)例程。

在此例程中，微型驱动程序无法例如解除分配帧、 完成的框架中，返回挂起的工作或重新填充并 reinject 帧。

若要设置注入模式，微型驱动程序调用[ **KsPinRegisterFrameReturnCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff563522) ，并提供一个指向其*AVStrMiniFrameReturn*例程。

*不要调用* ***KsPinRegisterFrameReturnCallback*** *除非筛选器处于停止状态。*

若要将帧注入到线路，请调用[ **KsPinSubmitFrame** ](https://msdn.microsoft.com/library/windows/hardware/ff563529)或[ **KsPinSubmitFrameMdl**](https://msdn.microsoft.com/library/windows/hardware/ff563530)。

下图显示了设置组成源筛选器，一个 AVStream 筛选器*就地*与源注入帧转换筛选器和呈现筛选器。

![说明 avstream 筛选器集的关系图](images/inject1.png)

 

 




