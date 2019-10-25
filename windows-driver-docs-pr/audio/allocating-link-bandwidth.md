---
title: 分配链路带宽
description: 分配链路带宽
ms.assetid: 7a5d5364-d869-4f6a-a7c3-9326ec347150
keywords:
- HD 音频，带宽
- 高清晰音频（HD 音频），带宽
- 总线带宽 WDK 音频
- 带宽 WDK 音频
- 分配带宽
- 链接带宽 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3b597c8a7682493a1455d6dcc8cb209a8e765a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831581"
---
# <a name="allocating-link-bandwidth"></a>分配链路带宽


HD 音频链接有有限数量的总线带宽可供呈现和捕获流使用。 为了确保 glitchless 音频，HD 音频总线驱动程序将总线带宽管理为共享资源。 当函数驱动程序分配 DMA 引擎时，它还必须为 DMA 引擎的呈现或捕获流分配一部分可用的总线带宽才能使用。

可在高清音频链接的串行数据（SDI）行和串行输出（SDO）行上使用固定的总线带宽量。 HD 音频总线驱动程序分别监视 SDI 和 SDO 行的带宽消耗。 如果分配输入或输出总线带宽的请求超出可用带宽，则总线驱动程序将无法请求。

当函数驱动程序调用 bus 驱动程序的[**AllocateCaptureDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)和[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)例程时，它将指定流格式。 流格式指定流的采样率、样本大小和通道数。 通过此信息，分配*Xxx*DmaEngine 例程确定流的总线带宽要求。 如果有足够的带宽可用，例程将为 DMA 引擎分配所需的带宽，以便使用。 否则，对分配*Xxx*DmaEngine 的调用将失败。

函数驱动程序可以调用[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)来请求更改现有 DMA 引擎分配的带宽分配。

可在两个版本的 HD 音频 DDI 中使用 "分配*Xxx*DmaEngine" 和 " [**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pchange_bandwidth_allocation) " 例程。

 

 




