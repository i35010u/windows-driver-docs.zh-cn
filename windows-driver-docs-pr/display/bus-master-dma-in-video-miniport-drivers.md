---
title: 主总线 DMA 视频微型端口驱动程序中
description: 主总线 DMA 视频微型端口驱动程序中
ms.assetid: fe6c2e16-d222-4948-b1df-34ed8d57d9d8
keywords:
- 微型端口驱动程序 WDK Windows 2000，总线 master DMA
- 主总线 DMA WDK 视频微型端口
- DMA 总线 master WDK 微型端口
- 常见缓冲区 DMA WDK 视频微型端口
- 常见缓冲区 DMA WDK 视频微型端口概述
- 基于数据包的 DMA WDK 微型端口
- 基于数据包的 DMA WDK 微型端口概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40297b11d5225031b27f20f20ea64e3d56532154
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521131"
---
# <a name="bus-master-dma-in-video-miniport-drivers"></a>主总线 DMA 视频微型端口驱动程序中


## <span id="ddk_bus_master_dma_in_video_miniport_drivers_gg"></span><span id="DDK_BUS_MASTER_DMA_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


从 Windows xp 中，则操作系统图形接口支持 PCI 总线 master 设备上 DMA。 PCI 总线母版设备的微型端口驱动程序可以实现以下类型的 DMA 支持使用提供的视频端口驱动程序的帮助程序函数：

-   **基于数据包的 DMA**

    基于数据包的 dma 数据请求方的空间和设备之间直接传输。 请求者的空间可能不是连续的因为基于数据包的 DMA 是与硬件散播-聚集支持这些设备上更高效。 基于数据包的 DMA 是用户空间和设备之间移动大量的任意数据的理想之选。

-   **常见缓冲区 DMA**

    在常见缓冲区 DMA 缓冲区共享之间 (因此，共有)，并由主机和 DMA 的反复运算的设备。 某些驱动程序使用常见缓冲区 DMA 将驱动程序操作的数据，例如一系列命令上, 传到图形引擎。 常见的缓冲区是连续并且始终可访问设备和主机 CPU。

    常见的缓冲区是宝贵的系统资源。 为了更好的整体驱动程序和系统性能，驱动程序应尽可能经济地使用常见缓冲区 DMA。

根据主机总线适配器的性质，某些微型端口驱动程序以独占方式使用基于数据包的 DMA、 其他人以独占方式，使用常见缓冲区 DMA 和一些同时使用。

无论使用哪种类型的 DMA，微型端口驱动程序应调用[ **VideoPortGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff570312)若要获取指向的指针[**副总裁\_DMA\_适配器**](https://msdn.microsoft.com/library/windows/hardware/ff570570)结构，并将其用于后续 DMA 函数调用。 微型端口驱动程序时不再需要 DMA 可以继续工作，应调用[ **VideoPortPutDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff570335)放弃该适配器对象。

以下各小节介绍如何使用提供的视频端口驱动程序的基于数据包的和常见缓冲区 DMA 支持。

[基于数据包的总线 Master DMA](packet-based-bus-master-dma.md)

[常见缓冲区总线 Master DMA](common-buffer-bus-master-dma.md)

[使用 DMA 时要考虑的点](points-to-consider-when-using-dma.md)

 

 





