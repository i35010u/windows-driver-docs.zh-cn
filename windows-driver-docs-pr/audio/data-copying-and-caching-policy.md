---
title: 数据复制和缓存策略
description: 数据复制和缓存策略
keywords:
- HD 音频，缓存
- 高清晰音频 (HD 音频) ，缓存
- 缓存 WDK 音频
- 总线侦听 WDK 音频
- 窥探 WDK 音频
- 内存 WDK 音频
- 复制音频数据
- 数据复制 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4323fe071ed46fa71e4380e2a1903612d332da90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784887"
---
# <a name="data-copying-and-caching-policy"></a>数据复制和缓存策略


WaveCyclic 微型端口驱动程序在 DMA 缓冲区（HD Audio 控制器硬件访问的）和客户端缓冲区之间复制音频数据，用户模式音频应用程序将访问这些数据：

-   对于播放数据流，驱动程序将数据从客户端缓冲区复制到 DMA 缓冲区。

-   对于捕获数据流，驱动程序将数据从 DMA 缓冲区复制到客户端缓冲区。

对于播放和捕获流，驱动程序可以启用 DMA 缓冲区内存 (缓存类型 **MmCached**) 的缓存，并依赖 PCI 控制器的总线侦听机制来确保缓存的一致性，从而实现最佳性能。 但是，某些 PCI Express 控制器实现不会使 HD 音频控制器的同步数据传输 (如 Intel 初始 PCI Express 芯片) 。

函数驱动程序无法检测 PCI 控制器硬件是否支持侦听 DMA 缓冲区传输或执行同步数据传输。 为了避免潜在的缓存一致性问题，驱动程序通过将该内存的缓存类型指定为 **MmWriteCombined** 来禁用 DMA 缓冲区内存的缓存。  (**MmNonCached** 也会运行，但也可能不会执行。 ) 如果你编写基于示例函数驱动程序的自定义适配器驱动程序，则 WaveCyclic 微型端口驱动程序应采用类似方式，除非你可以验证 PCI 控制器确实支持侦听 DMA 缓冲区传输。

若要支持不执行总线侦听的设备和系统，自定义函数驱动程序必须遵循以下规则：

-   对于播放流，将 DMA 缓冲区的缓存类型指定为 **MmWriteCombined**。 将数据块从客户端缓冲区复制到 DMA 缓冲区后，调用 [**KeMemoryBarrier**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kememorybarrier) 函数使数据对 dma 引擎可见。 **KeMemoryBarrier** 以一种高效的方式将复制的数据刷新到内存，这会使处理器的数据缓存很大程度上不受影响。

-   对于捕获流，将 DMA 缓冲区的缓存类型指定为 **MmWriteCombined** 或 **MmNonCached**。 此外，函数驱动程序应避免写入 DMA 缓冲区。 如果必须对音频示例执行就地处理，则应首先将数据复制到其他位置。

函数驱动程序复制到 DMA 缓冲区或从 DMA 缓冲区复制的数据块无需在写入合并缓冲区边界上开始或结束，并且其大小不需要为写入合并缓冲区大小的倍数 (通常为32或64字节) 。

对于使用 DDI 的 [**HDAUDIO \_ BUS \_ INTERFACE \_ BDL**](/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl) 版本的编解码器函数驱动程序， [**AllocateContiguousDmaBuffer**](/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer) 例程将同时执行 DMA 缓冲区内存的分配和映射。 例程始终将缓冲区的缓存类型设置为 **MmWriteCombined**。

有关写入合并的详细信息，请参阅 [intel](https://www.intel.com/content/www/us/en/homepage.html) 网站上的 IA-32 Intel 体系结构软件开发人员手册。

 

