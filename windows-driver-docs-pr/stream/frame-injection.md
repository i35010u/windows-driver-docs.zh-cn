---
title: 帧注入
description: 帧注入
keywords:
- 帧 WDK AVStream
- 注入模式 WDK AVStream 帧
- 帧注入 WDK AVStream
- pin 中心筛选器 WDK AVStream
- 以筛选为中心的筛选器 WDK AVStream
- 空帧 WDK AVStream
- 默认帧行为 WDK AVStream
- 覆盖默认帧行为 WDK 流式处理媒体
- 线路 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01fde074e3b1e80e49d480800ab83ed717942563
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840263"
---
# <a name="frame-injection"></a>帧注入





默认情况下，在 AVStream 中，请求程序从分配器获取空帧，并将其放在队列中。 然后，微型驱动程序将使用以 [零为中心的处理](pin-centric-processing.md) 或以 [筛选为中心的处理](filter-centric-processing.md)来填充帧。 帧会移动到线路中的下一个对象，最终完成线路并返回给请求者。 然后，AVStream 重用这些帧。

微型驱动程序可以使用 *注入模式* 替代此默认行为。 在注入模式下，微型驱动程序负责将帧放置到线路中。 帧以默认方式传播到线路。 当帧返回到其开始位置的 AVStream 对象时，AVStream 会调用微型驱动程序提供的 [*AVStrMiniFrameReturn*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinframereturn) 例程。

在这种情况下，微型驱动程序可能会导致解除分配帧的操作、完成帧返回时挂起的工作或重填和 reinject 帧。

若要设置注入模式，微型驱动程序将调用 [**KsPinRegisterFrameReturnCallback**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinregisterframereturncallback) 并提供指向其 *AVStrMiniFrameReturn* 例程的指针。

不 *调用*  ***KsPinRegisterFrameReturnCallback** _ _unless 筛选器处于停止状态。 *

若要将帧插入线路，请调用 [**KsPinSubmitFrame**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinsubmitframe) 或 [**KsPinSubmitFrameMdl**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinsubmitframemdl)。

下图显示了由源筛选器、 *就地* 转换筛选器和包含源注入帧的呈现筛选器组成的 AVStream 筛选器集。

![说明 avstream 筛选器集的关系图](images/inject1.png)

 

