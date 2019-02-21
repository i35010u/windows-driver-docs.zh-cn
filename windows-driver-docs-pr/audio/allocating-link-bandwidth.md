---
title: 分配链路带宽
description: 分配链路带宽
ms.assetid: 7a5d5364-d869-4f6a-a7c3-9326ec347150
keywords:
- HD Audio、 带宽
- 高清晰度音频 (HD Audio)、 带宽
- 总线带宽 WDK 音频
- 带宽 WDK 音频
- 分配的带宽
- 链接带宽 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49e7c4082d6a4ab11ac7d1cc376e03a29af2a66e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556068"
---
# <a name="allocating-link-bandwidth"></a>分配链路带宽


HD 音频链接具有有限的总线带宽可用于呈现和捕获使用的流。 若要确保 glitchless 音频，HD Audio 总线驱动程序管理总线带宽为共享资源。 当功能驱动程序分配的 DMA 引擎时，它必须还 DMA 引擎的呈现器为分配一部分可用总线带宽或捕获要使用流。

HD 音频链接 (SDI) 行中的串行数据和串行输出数据量 (SDO) 行上提供了固定的总线带宽量。 HD Audio 总线驱动程序监视 SDI 和 SDO 行上单独的带宽消耗。 如果请求无法分配输入或输出总线带宽超过可用带宽，总线驱动程序会使请求失败。

当功能驱动程序调用总线驱动程序[ **AllocateCaptureDmaEngine** ](https://msdn.microsoft.com/library/windows/hardware/ff536177)并[ **AllocateRenderDmaEngine** ](https://msdn.microsoft.com/library/windows/hardware/ff536181)例程，它指定流格式。 流格式指定流的采样率、 示例大小以及通道数。 中的信息，分配*Xxx*DmaEngine 例程确定流的总线带宽要求。 如果有足够的带宽可用，例程分配要使用的 DMA 引擎所需的带宽。 否则为对分配的调用*Xxx*DmaEngine 失败。

功能驱动程序可以调用[ **ChangeBandwidthAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff536229)请求中现有的 DMA 引擎分配的带宽分配的更改。

分配*Xxx*DmaEngine 和[ **ChangeBandwidthAllocation** ](https://msdn.microsoft.com/library/windows/hardware/ff536229)例程是 HD 音频 DDI 的这两个版本中可用。

 

 




