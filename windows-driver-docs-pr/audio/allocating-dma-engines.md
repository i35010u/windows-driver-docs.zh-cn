---
title: 分配 DMA 引擎
description: 分配 DMA 引擎
ms.assetid: 45b772ce-e6ae-4102-bad4-734f8f079817
keywords:
- HD 音频，DMA 引擎
- 高清晰音频 (HD 音频) ，DMA 引擎
- 分配 DMA 引擎
- DMA 引擎分配 WDK 音频
- 呈现 DMA 引擎 WDK 音频
- 捕获 DMA 引擎 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c29b0d8a2db99cbb84e4e51b667e11abfd2e3e2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208377"
---
# <a name="allocating-dma-engines"></a>分配 DMA 引擎


HD 音频控制器包含固定数量的 DMA 引擎。 每个引擎都可以对单个呈现或捕获流执行分散/收集传输。

有三种类型的 DMA 引擎可用：

-   呈现 DMA 引擎，它们只能处理渲染流。

-   捕获 DMA 引擎，它们只能处理捕获流。

-   双向 DMA 引擎，可配置为处理渲染或捕获流。

为呈现流分配 DMA 引擎时， [**AllocateCaptureDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_capture_dma_engine) 例程会分配一个呈现 dma 引擎（如果有）。 如果呈现 DMA 引擎的供应用完，则例程将分配双向 DMA 引擎（如果有）。

同样，为捕获流分配 DMA 引擎时， [**AllocateRenderDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine) 例程会分配一个捕获 DMA 引擎（如果有）。 如果捕获 DMA 引擎的供应用完了，例程将分配一个双向 DMA 引擎（如果有）。

可在两个版本的 HD audio DDI 中使用 "分配*Xxx*DmaEngine" 例程。

 

