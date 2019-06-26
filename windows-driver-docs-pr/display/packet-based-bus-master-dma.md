---
title: 基于数据包的总线主控 DMA
description: 基于数据包的总线主控 DMA
ms.assetid: f94b9ca9-6e29-4801-a092-30af19345f6d
keywords:
- 主总线 DMA WDK 微型端口，基于数据包
- DMA 总线 master WDK 微型端口，基于数据包
- 基于数据包的 DMA WDK 微型端口说明
- VideoPortStartDma
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd0e6a30fbf57f1dce2dc4ba7c2c14121862cc51
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377383"
---
# <a name="packet-based-bus-master-dma"></a>基于数据包的总线主控 DMA


## <span id="ddk_packet_based_bus_master_dma_gg"></span><span id="DDK_PACKET_BASED_BUS_MASTER_DMA_GG"></span>


通常，显示器驱动程序通过将传输请求发送到微型端口驱动程序启动 DMA 操作。 当支持基于数据包的 DMA 操作的微型端口驱动程序收到此类请求时，它首先锁定数据传输所涉及的缓冲区。 微型端口驱动程序然后通过调用的视频端口驱动程序的启动传输[ **VideoPortStartDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstartdma)函数，后者又调用微型端口驱动程序[ **HwVidExecuteDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pexecute_dma)回调例程来执行数据传输。 以异步方式处理此 DMA 操作：**VideoPortStartDma**不会等待 DMA 操作完成之前将控制权返还给微型端口驱动程序。

具体取决于传输请求和系统资源分配给的适配器数的大小，该驱动程序可能不能传输的所有单个 DMA 操作数据。 微型端口驱动程序应检查以确定是否返回的实际传输大小更多的数据传输。 只要 DMA 硬件完毕当前传输，微型端口驱动程序应调用的视频端口驱动程序[ **VideoPortCompleteDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportcompletedma)函数来完成当前的 DMA 操作。 如果仍然要传输的剩余数据，微型端口驱动程序将重复调用的视频端口驱动程序的过程**VideoPortStartDma**并**VideoPortCompleteDma**以迭代方式函数直到没有更多数据将保留传输。 当已传输的所有数据时，微型端口驱动程序应取消锁定缓冲区。

微型端口驱动程序将执行以下一系列操作，使用基于数据包的 DMA:

1.  向系统中报告的硬件功能，并且获取适配器对象。

    微型端口驱动程序调用的视频端口驱动程序[ **VideoPortGetDmaAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportgetdmaadapter)函数，返回一个指向[**副总裁\_DMA\_适配器**](https://docs.microsoft.com/previous-versions/ff570570(v=vs.85))结构。 这通常是在初始化时，通常在微型端口驱动程序[ *HwVidFindAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)例程。 微型端口驱动程序将此指针用于后续 DMA 操作。

2.  锁定主机内存。

    微型端口驱动程序调用的视频端口驱动程序[ **VideoPortLockBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportlockbuffer)函数，探测缓冲区，使得这些内存页驻留，并将其锁定。

3.  开始 DMA 传输。

    微型端口驱动程序调用的视频端口驱动程序[ **VideoPortStartDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstartdma)函数，刷新主机处理器内存缓存中，生成散播-聚集列表中，并调用微型端口驱动[**HwVidExecuteDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pexecute_dma)以异步方式执行 DMA 的操作的回调例程。 **VideoPortStartDma**将控制权返回给微型端口驱动程序，而无需等待 DMA 操作完成。

4.  完成 DMA 传输。

    微型端口驱动程序应调用的视频端口驱动程序[ **VideoPortCompleteDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportcompletedma)函数只要硬件完毕 DMA 操作。 DMA 操作完成时，视频适配器的数量生成中断。 例如，具有此类型的适配器的系统无法响应中断如下所示。 当硬件生成中断通知 DMA 操作已完成的微型端口驱动程序时，微型端口驱动程序的中断服务例程 (ISR) 调用的视频端口驱动程序[ **VideoPortQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportqueuedpc)函数进行排队 DPC 例程，后者又调用的视频端口驱动程序**VideoPortCompleteDma**函数。 不能直接调用 ISR **VideoPortCompleteDma**因为此视频端口驱动程序函数必须等于或低于 IRQL 调度调用\_级别。

    **VideoPortCompleteDma**刷新主机总线适配器的内部缓存中剩余的任何数据，并释放任何未使用的资源 (包括生成的分散/聚拢列表**VideoPortStartDma**)。

    如果只有部分数据转移 （由于可用的映射注册数的限制），微型端口驱动程序必须进行重复的调用**VideoPortStartDma**和**VideoPortCompleteDma**直到已转移的所有数据。

5.  解锁主机内存。

    当已传输的所有数据时，微型端口驱动程序应调用的视频端口驱动程序[ **VideoPortUnlockBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportunlockbuffer)函数解锁它在第二个步骤中获取的数据缓冲区。

6.  放弃该适配器对象。

    *此步骤是可选的*。 如果由于某种原因，微型端口驱动程序决定将其剩余生存期内没有进一步 DMA 操作，应通过调用的视频端口驱动程序丢弃 DMA 适配器对象[ **VideoPortPutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportputdmaadapter)函数。

 

 





