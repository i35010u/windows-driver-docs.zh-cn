---
title: 基于数据包的总线主控 DMA
description: 基于数据包的总线主控 DMA
ms.assetid: f94b9ca9-6e29-4801-a092-30af19345f6d
keywords:
- 总线主控 DMA WDK 音频视频微型端口，基于数据包
- DMA 总线-主 WDK 视频微型端口，基于数据包
- 基于数据包的 DMA WDK 视频微型端口，说明
- VideoPortStartDma
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b84201c0c01738ef9865796fdc04a4d43164276
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826061"
---
# <a name="packet-based-bus-master-dma"></a>基于数据包的总线主控 DMA


## <span id="ddk_packet_based_bus_master_dma_gg"></span><span id="DDK_PACKET_BASED_BUS_MASTER_DMA_GG"></span>


通常，显示驱动程序通过将传输请求发送到微型端口驱动程序来启动 DMA 操作。 当支持基于数据包的 DMA 操作的微型端口驱动程序收到此类请求时，它将首先锁定数据传输中涉及的缓冲区。 然后，微型端口驱动程序通过调用视频端口驱动程序的[**VideoPortStartDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportstartdma)函数来启动传输，后者又调用微型端口驱动程序的[**HwVidExecuteDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pexecute_dma)回调例程来执行数据传输。 此 DMA 操作以异步方式进行处理： **VideoPortStartDma**在将控制权返回给微型端口驱动程序之前，不会等待 DMA 操作完成。

根据传输请求的大小和分配给适配器的系统资源数，驱动程序可能无法在单个 DMA 操作中传输所有数据。 小型端口驱动程序应检查返回的实际传输大小，以确定是否有更多的数据要传输。 DMA 硬件完成当前传输后，微型端口驱动程序应调用视频端口驱动程序的[**VideoPortCompleteDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcompletedma)函数来完成当前 DMA 操作。 如果仍有要传输的数据，微型端口驱动程序将重复调用视频端口驱动程序的**VideoPortStartDma**和**VideoPortCompleteDma**函数，直到不再传输更多的数据。 传输所有数据后，微型端口驱动程序应解锁缓冲区。

微型端口驱动程序执行以下一系列操作以使用基于数据包的 DMA：

1.  向系统报告硬件功能并获取适配器对象。

    微型端口驱动程序调用视频端口驱动程序的[**VideoPortGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetdmaadapter)函数，该函数返回指向[**VP\_DMA\_适配器**](https://docs.microsoft.com/previous-versions/ff570570(v=vs.85))结构的指针。 通常在初始化时完成此操作，通常在微型端口驱动程序的[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)例程内完成。 小型端口驱动程序使用此指针执行后续的 DMA 操作。

2.  锁定主机内存。

    微型端口驱动程序调用视频端口驱动程序的[**VideoPortLockBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportlockbuffer)函数，该函数探测缓冲区，使这些内存页驻留在一起，并对它们进行锁定。

3.  开始 DMA 传输。

    微型端口驱动程序调用视频端口驱动程序的[**VideoPortStartDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportstartdma)函数，该函数将刷新主机处理器内存缓存，生成散点/集合列表，并调用微型端口驱动程序的[**HwVidExecuteDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pexecute_dma)回调例程来执行DMA 操作的异步操作。 **VideoPortStartDma**将控制权返回给微型端口驱动程序，而无需等待 DMA 操作完成。

4.  完成 DMA 传输。

    硬件完成 DMA 操作后，微型端口驱动程序应立即调用视频端口驱动程序的[**VideoPortCompleteDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcompletedma)函数。 许多视频适配器在 DMA 操作完成时生成中断。 例如，具有此类型的适配器的系统可通过以下方式对中断做出反应。 当硬件生成中断以便通知微型端口驱动程序 DMA 操作已完成时，微型端口驱动程序的中断服务例程（ISR）会调用视频端口驱动程序的[**VideoPortQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportqueuedpc)函数来对 DPC 例程进行排队，请调用视频端口驱动程序的**VideoPortCompleteDma**函数。 ISR 无法直接调用**VideoPortCompleteDma** ，因为此视频端口驱动程序函数必须在 IRQL 调度\_级别调用或低于 IRQL 调度。

    **VideoPortCompleteDma**刷新总线主适配器的内部缓存中剩余的所有数据，并释放所有未使用的资源（包括由**VideoPortStartDma**生成的散点/集合列表）。

    如果只传输部分数据（例如，由于可用映射寄存器数的限制），微型端口驱动程序必须对**VideoPortStartDma**和**VideoPortCompleteDma**进行重复调用，直到所有数据都已此前.

5.  解锁主机内存。

    传输所有数据后，微型端口驱动程序应调用视频端口驱动程序的[**VideoPortUnlockBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportunlockbuffer)函数来解锁第二步中获取的数据缓冲区。

6.  丢弃适配器对象。

    *此步骤是可选的*。 如果由于某种原因，微型端口驱动程序决定在其生存期的其余部分不会有进一步的 DMA 操作，则应通过调用视频端口驱动程序的[**VideoPortPutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportputdmaadapter)函数来放弃 dma 适配器对象。

 

 





