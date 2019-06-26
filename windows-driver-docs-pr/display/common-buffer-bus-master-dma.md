---
title: 公用缓冲区总线主控 DMA
description: 公用缓冲区总线主控 DMA
ms.assetid: 4758e084-1d9e-4e17-8627-05edc6b664ba
keywords:
- 主总线 DMA WDK 微型端口，常见的缓冲区
- DMA 总线 master WDK 微型端口，常见的缓冲区
- 常见缓冲区 DMA WDK 微型端口说明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b802004ff876bdf367e8f5378d755a8b0650fbf8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370670"
---
# <a name="common-buffer-bus-master-dma"></a>公用缓冲区总线主控 DMA


## <span id="ddk_common_buffer_bus_master_dma_gg"></span><span id="DDK_COMMON_BUFFER_BUS_MASTER_DMA_GG"></span>


微型端口驱动程序将执行以下一系列操作，使用常见缓冲区 DMA:

1.  获取适配器对象。

    微型端口驱动程序调用的视频端口驱动程序[ **VideoPortGetDmaAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportgetdmaadapter)函数，通常在微型端口驱动程序[ *HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)例程，以获取指向的指针[**副总裁\_DMA\_适配器**](https://docs.microsoft.com/previous-versions/ff570570(v=vs.85))结构。 微型端口驱动程序将此指针用于后续 DMA 操作。

2.  分配常见的缓冲区。

    微型端口驱动程序调用的视频端口驱动程序[ **VideoPortAllocateCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportallocatecommonbuffer)函数，请使用上一步中获取的指针。

3.  释放常见的缓冲区。

    当微型端口驱动程序不再需要时常见的缓冲区时，它将调用的视频端口驱动程序[ **VideoPortReleaseCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportreleasecommonbuffer)函数。

4.  放弃该适配器对象。

    此步骤可选。 如果由于某种原因，微型端口驱动程序决定将其剩余生存期内没有进一步 DMA 操作，应通过调用的视频端口驱动程序丢弃 DMA 适配器对象[ **VideoPortPutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportputdmaadapter)函数。

 

 





