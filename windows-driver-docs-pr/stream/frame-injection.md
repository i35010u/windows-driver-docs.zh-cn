---
title: 帧注入
description: 帧注入
ms.assetid: cdfb1763-92a8-4a60-8f49-2af34a8beca5
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
ms.openlocfilehash: b35de0fd7d27bd90a4ea6f1c40b846cd224b6563
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842596"
---
# <a name="frame-injection"></a>帧注入





默认情况下，在 AVStream 中，请求程序从分配器获取空帧，并将其放在队列中。 然后，微型驱动程序将使用以[零为中心的处理](pin-centric-processing.md)或以[筛选为中心的处理](filter-centric-processing.md)来填充帧。 帧会移动到线路中的下一个对象，最终完成线路并返回给请求者。 然后，AVStream 重用这些帧。

微型驱动程序可以使用*注入模式*替代此默认行为。 在注入模式下，微型驱动程序负责将帧放置到线路中。 帧以默认方式传播到线路。 当帧返回到其开始位置的 AVStream 对象时，AVStream 会调用微型驱动程序提供的[*AVStrMiniFrameReturn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinframereturn)例程。

在这种情况下，微型驱动程序可能会导致解除分配帧的操作、完成帧返回时挂起的工作或重填和 reinject 帧。

若要设置注入模式，微型驱动程序将调用[**KsPinRegisterFrameReturnCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinregisterframereturncallback)并提供指向其*AVStrMiniFrameReturn*例程的指针。

*除非筛选器处于停止状态*，否则*不要调用* ***KsPinRegisterFrameReturnCallback*** 。

若要将帧插入线路，请调用[**KsPinSubmitFrame**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinsubmitframe)或[**KsPinSubmitFrameMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinsubmitframemdl)。

下图显示了由源筛选器、*就地*转换筛选器和包含源注入帧的呈现筛选器组成的 AVStream 筛选器集。

![说明 avstream 筛选器集的关系图](images/inject1.png)

 

 




