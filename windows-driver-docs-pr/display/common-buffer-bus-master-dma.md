---
title: 公用缓冲区总线主控 DMA
description: 公用缓冲区总线主控 DMA
ms.assetid: 4758e084-1d9e-4e17-8627-05edc6b664ba
keywords:
- 总线主控 DMA WDK 音频视频微型端口，公共缓冲区
- DMA 总线-主 WDK 视频微型端口，公共缓冲区
- 常见缓冲区 DMA WDK 视频微型端口，说明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0076fd8238bb9f254222d35265a77468c21388e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839800"
---
# <a name="common-buffer-bus-master-dma"></a>公用缓冲区总线主控 DMA


## <span id="ddk_common_buffer_bus_master_dma_gg"></span><span id="DDK_COMMON_BUFFER_BUS_MASTER_DMA_GG"></span>


微型端口驱动程序执行以下操作序列来使用常见缓冲区 DMA：

1.  获取适配器对象。

    微型端口驱动程序调用视频端口驱动程序的[**VideoPortGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetdmaadapter)函数，通常在微型端口驱动程序的[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)例程内，以获取指向[**VP\_DMA\_适配器**](https://docs.microsoft.com/previous-versions/ff570570(v=vs.85))结构的指针。 小型端口驱动程序使用此指针执行后续的 DMA 操作。

2.  分配公共缓冲区。

    微型端口驱动程序使用上一步中获取的指针调用视频端口驱动程序的[**VideoPortAllocateCommonBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportallocatecommonbuffer)函数。

3.  释放公共缓冲区。

    当微型端口驱动程序不再需要通用缓冲区时，它将调用视频端口驱动程序的[**VideoPortReleaseCommonBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportreleasecommonbuffer)函数。

4.  丢弃适配器对象。

    此步骤可选。 如果由于某种原因，微型端口驱动程序决定在其生存期的其余部分不会有进一步的 DMA 操作，则应通过调用视频端口驱动程序的[**VideoPortPutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportputdmaadapter)函数来放弃 dma 适配器对象。

 

 





