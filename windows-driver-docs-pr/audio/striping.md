---
title: 条带化
description: 条带化
keywords:
- 带化 WDK 音频
- HD 音频，条带化
- 高清晰音频 (HD 音频) ，条带化
- HD 音频，带宽
- 高清晰音频 (HD 音频) ，带宽
- 总线带宽 WDK 音频
- 带宽 WDK 音频
- 分配带宽
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5813aa424a6a64624590b722a2862a85fb93620b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802097"
---
# <a name="striping"></a>条带化


HD 音频体系结构支持一种称为 *条带化* 技术，可减少呈现流使用的总线带宽量。 如果 HD 音频硬件接口提供了多个 SDO 线路，则条带化可以通过交替地将数据流中的位分散到 SDO 行中来增加呈现 DMA 引擎传输数据的速度。 第一位 (最重要的位) 通过 SDO0 传播，第二位通过 SDO1，依此类推。 例如，对于两个 SDO 行，条带化可以通过在两个 SDO 行之间拆分流来有效地将传输速率加倍。 使用条带化在两个 SDO 线路上传输渲染流的 DMA 引擎仅消耗一半的总线带宽（如果它未使用条带）。

函数驱动程序通过 [**AllocateRenderDmaEngine**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine) 例程的 *条带* 调用参数启用条带化。

有关条带化的详细信息，请参阅 [INTEL HD 音频](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html)网站上的 *Intel 高质音频规范*。

 

