---
title: 条带化
description: 条带化
ms.assetid: 29ab650c-0c3b-4693-a277-4d9ba63b7b66
keywords:
- 带化 WDK 音频
- HD 音频，条带化
- 高清晰音频（HD 音频），条带化
- HD 音频，带宽
- 高清晰音频（HD 音频），带宽
- 总线带宽 WDK 音频
- 带宽 WDK 音频
- 分配带宽
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a002afac326d572af80849061048870fa59a651
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830106"
---
# <a name="striping"></a>条带化


HD 音频体系结构支持一种称为*条带化*技术，可减少呈现流使用的总线带宽量。 如果 HD 音频硬件接口提供了多个 SDO 线路，则条带化可以通过交替地将数据流中的位分散到 SDO 行中来增加呈现 DMA 引擎传输数据的速度。 第一位（最高有效位）通过 SDO0 传播，第二位通过 SDO1，依此类推。 例如，对于两个 SDO 行，条带化可以通过在两个 SDO 行之间拆分流来有效地将传输速率加倍。 使用条带化在两个 SDO 线路上传输渲染流的 DMA 引擎仅消耗一半的总线带宽（如果它未使用条带）。

函数驱动程序通过[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)例程的*条带*调用参数启用条带化。

有关条带化的详细信息，请参阅[INTEL HD 音频](https://go.microsoft.com/fwlink/p/?linkid=42508)网站上的*Intel 高质音频规范*。

 

 




