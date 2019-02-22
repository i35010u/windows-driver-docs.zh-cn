---
title: 数据复制和缓存策略
description: 数据复制和缓存策略
ms.assetid: 1867f2bd-240c-4525-9f02-98b8f1d54b17
keywords:
- HD Audio 缓存
- 高清晰度音频 (HD Audio) 缓存
- 缓存 WDK 音频
- 总线窥探 WDK 音频
- 探寻 WDK 音频
- 内存 WDK 音频
- 将音频数据复制
- 数据复制 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3b30cd4100680fe5c63baead176a92dff530771
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533179"
---
# <a name="data-copying-and-caching-policy"></a>数据复制和缓存策略


WaveCyclic 微型端口驱动程序将复制 HD Audio 控制器硬件访问，DMA 缓冲区和用户模式音频应用程序访问的客户端缓冲区之间的音频数据：

-   对于播放数据流，该驱动程序将数据复制从客户端缓冲区到 DMA 缓冲区。

-   对于捕获数据流，该驱动程序将数据复制从 DMA 缓冲区到客户端缓冲区。

播放和捕获的流，该驱动程序可以获得最佳性能的启用 DMA 缓冲区内存的缓存 (缓存类型**MmCached**)，并依赖于 PCI 控制器的总线搜寻机制来确保缓存一致性。 但是，某些 PCI Express 控制器实现不搜索 HD Audio 控制器的同步数据传输 （如 Intel 的初始 PCI Express 芯片组）。

功能驱动程序无法检测 PCI 控制器硬件是否支持搜寻的 DMA 缓冲区传输或执行同步数据传输。 若要避免缓存协调性的潜在问题，该驱动程序禁用缓存 DMA 缓冲区内存的通过指定为该内存的缓存类型**MmWriteCombined**。 (**MmNonCached**也将起作用，但也可能无法执行。)如果编写基于示例函数驱动程序的自定义适配器驱动程序，除非可以验证 PCI 控制器确实实际上支持搜寻的 DMA 缓冲区传输 WaveCyclic 微型端口驱动程序应同样行为。

若要支持设备和系统不执行总线搜寻的自定义功能驱动程序必须遵循下列规则：

-   对于播放流，DMA 缓冲区缓存类型指定为**MmWriteCombined**。 从客户端缓冲区的数据块复制到 DMA 缓冲区之后, 调用[ **KeMemoryBarrier** ](https://msdn.microsoft.com/library/windows/hardware/ff552971)函数以使数据显示到 DMA 引擎。 **KeMemoryBarrier**将复制的数据刷新到内存，在离开处理器的数据缓存很大程度上受影响的有效方法。

-   对于捕获的流，DMA 缓冲区缓存类型指定为任一**MmWriteCombined**或**MmNonCached**。 此外，功能驱动程序应避免向 DMA 缓冲区写入。 如果它必须执行适当地处理的音频示例，它应首先复制到其他位置的数据。

功能驱动程序复制到或从 DMA 缓冲区的数据块的不需要开头或结尾在写组合缓冲区边界和其大小不需要是写组合的缓冲区大小 （通常情况下，32 或 64 字节） 的倍数。

使用的编解码器函数驱动程序[ **HDAUDIO\_总线\_接口\_BDL** ](https://msdn.microsoft.com/library/windows/hardware/ff536416) DDI 版本[ **AllocateContiguousDmaBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff536178)例程执行分配和 DMA 缓冲区内存的映射。 例程总是缓冲区的缓存类型设置为**MmWriteCombined**。

有关写组合的详细信息，请参阅在 IA-32 Intel 体系结构软件开发人员手册[Intel](https://go.microsoft.com/fwlink/p/?linkid=38518)网站。

 

 




