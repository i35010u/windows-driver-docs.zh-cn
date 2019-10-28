---
title: 视频微型端口驱动程序中的总线主控 DMA
description: 视频微型端口驱动程序中的总线主控 DMA
ms.assetid: fe6c2e16-d222-4948-b1df-34ed8d57d9d8
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，主线-主 DMA
- 总线主控 DMA WDK 音频视频微型端口
- DMA 总线-主 WDK 视频微型端口
- 常见缓冲区 DMA WDK 视频微型端口
- 常见缓冲区 DMA WDK 视频微型端口，概述
- 基于数据包的 DMA WDK 视频微型端口
- 基于数据包的 DMA WDK 视频微型端口，概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6992915d543f886e4ba23d7a2355078a6262d7a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839822"
---
# <a name="bus-master-dma-in-video-miniport-drivers"></a>视频微型端口驱动程序中的总线主控 DMA


## <span id="ddk_bus_master_dma_in_video_miniport_drivers_gg"></span><span id="DDK_BUS_MASTER_DMA_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


从 Windows XP 开始，操作系统图形界面支持 PCI 总线主控设备上的 DMA。 PCI 总线主控设备的视频微型端口驱动程序可以使用视频端口驱动程序提供的 helper 函数实现以下类型的 DMA 支持：

-   **基于数据包的 DMA**

    在基于数据包的 DMA 中，数据直接在请求方的空间和设备之间传输。 由于请求者的空间可能不是连续的，因此，基于数据包的 DMA 在具有硬件散播/采集支持的设备上更有效。 基于数据包的 DMA 是在用户空间和设备之间移动大量任意数据的理想选择。

-   **常见缓冲区 DMA**

    在公用缓冲区 DMA 中，在（因此，公共到）之间共享缓冲区，并由主机和设备用于重复 DMA 操作。 某些驱动程序使用公用缓冲区 DMA 将驱动程序操作的数据（如一系列命令）上传到图形引擎。 公用缓冲区是连续的，并且始终可由设备和主机 CPU 访问。

    常见的缓冲区是宝贵的系统资源。 为了获得更好的整体驱动程序和系统性能，驱动程序应尽可能经济地使用公用缓冲区 DMA。

根据总线主适配器的性质，某些微型端口驱动程序以独占方式使用基于数据包的 DMA，而另一些则使用公用缓冲区 DMA。

无论使用哪种类型的 DMA，微型端口驱动程序都应调用[**VideoPortGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetdmaadapter) ，以获取指向[**VP\_DMA\_适配器**](https://docs.microsoft.com/previous-versions/ff570570(v=vs.85))结构的指针，并将其用于后续的 DMA 函数调用。 如果不再需要继续 DMA 操作，微型端口驱动程序应调用[**VideoPortPutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportputdmaadapter)来放弃适配器对象。

以下小节介绍了如何使用视频端口驱动程序提供的基于数据包和常见的缓冲区 DMA 支持。

[基于数据包的总线主机 DMA](packet-based-bus-master-dma.md)

[公用缓冲区总线主机 DMA](common-buffer-bus-master-dma.md)

[使用 DMA 时要考虑的要点](points-to-consider-when-using-dma.md)

 

 





