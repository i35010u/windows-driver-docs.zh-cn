---
title: 分配 DMA 引擎
description: 分配 DMA 引擎
ms.assetid: 45b772ce-e6ae-4102-bad4-734f8f079817
keywords:
- HD Audio，DMA 引擎
- 高清晰度音频 (HD Audio) DMA 引擎
- 分配 DMA 引擎
- DMA 引擎分配 WDK 音频
- 呈现 DMA 引擎 WDK 音频
- 捕获 DMA 引擎 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0040102cbb768bbb5a972f70e1c1272fb6cf4d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355768"
---
# <a name="allocating-dma-engines"></a>分配 DMA 引擎


HD Audio 控制器包含固定的数量的 DMA 引擎。 每个引擎可以执行的单个渲染散播-聚集传输或捕获流。

提供了三种类型的 DMA 引擎：

-   呈现 DMA 引擎，它可以处理仅呈现流。

-   捕获 DMA 引擎，它可以处理只捕获流。

-   双向 DMA 引擎，可以配置为处理任一呈现或捕获流。

对于呈现流，分配的 DMA 引擎时[ **AllocateCaptureDmaEngine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)例程分配渲染 DMA 引擎，如果有可用。 如果可以提供的呈现 DMA 引擎是已用完，如果可用，例程分配双向 DMA 引擎。

同样，当分配 DMA 引擎对于捕获的流， [ **AllocateRenderDmaEngine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_render_dma_engine)例程分配捕获 DMA 引擎，如果有可用。 如果提供捕获 DMA 引擎是已用完，如果可用，例程分配双向 DMA 引擎。

分配*Xxx*DmaEngine 例程是 HD 音频 DDI 的这两个版本中可用。

 

 




