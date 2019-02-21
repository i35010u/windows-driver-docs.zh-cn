---
title: WavePci 延迟
description: WavePci 延迟
ms.assetid: 6d83c015-cf8f-40b4-bf28-de865a5bfe2d
keywords:
- WavePci 延迟 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 718b7707eb0aa0d5cd51b0a06e8c30d30bbc05f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534160"
---
# <a name="wavepci-latency"></a>WavePci 延迟


## <span id="wavepci_latency"></span><span id="WAVEPCI_LATENCY"></span>


WavePci 端口驱动程序处理以不同的方式从 WaveCyclic 驱动程序的音频流的缓冲。

如果 WavePci 微型端口驱动程序提供了混合使用的硬件，DirectSound 将提交到 WavePci 端口驱动程序包含在一个循环缓冲区中的整个 DirectSound 批流 IRP。 DirectSound 分配作为一个连续的虚拟内存块的缓冲区。 若要避免复制 DirectSound 缓冲区，内核流式处理层将缓冲区映射到内核模式虚拟内存，并生成循环缓冲区中指定的内存页的虚拟和物理地址 MDL （内存描述符列表）。 WavePci 端口驱动程序转换为分配器帧序列分区循环缓冲区 (请参阅[KS 分配器](https://msdn.microsoft.com/library/windows/hardware/ff567257))。 微型端口驱动程序指定其首选的分配器帧大小及其[ **IMiniportWavePciStream::GetAllocatorFraming** ](https://msdn.microsoft.com/library/windows/hardware/ff536726)流初始化期间通过端口驱动程序调用方法。 但是，SysAudio，系统图生成器，可以重写以适应音频筛选器关系图中的其他组件的要求的微型端口驱动程序的首选项。

WavePci 端口驱动程序公开为一系列映射到微型端口驱动程序的循环缓冲区。 映射是整个分配框架的一部分。 如果特定分配框架存在于完全在页面内，则端口驱动程序将显示一个映射，并且微型端口驱动程序的帧。 如果分配帧跨越一个或多个页边界，端口驱动程序拆分每个页边界上的帧，并显示，并且两个或多个映射。 每次调用[ **IPortWavePciStream::GetMapping** ](https://msdn.microsoft.com/library/windows/hardware/ff536909)生成序列中的下一步后续映射。

与 WaveCyclic 情况下，其中微型端口驱动程序没有多大控制的毫秒数的数据通过缓冲在硬件，相比 WavePci 微型端口驱动程序具有它在任何时候具有打开的映射的数量相当大的控制权。 打开映射的数量会增加一个每次调用[ **GetMapping** ](https://msdn.microsoft.com/library/windows/hardware/ff536909)和一个每次调用都会减少[ **ReleaseMapping** ](https://msdn.microsoft.com/library/windows/hardware/ff536911). (A **GetMapping**调用可能会失败，当然，因此驱动程序未达到完全控制映射的数量。)通过控制打开映射的数量和跟踪的累计的映射的大小微型端口驱动程序可以确定 （在依赖于映射大小容差） 的缓冲的毫秒数可供硬件。 WavePci 微型端口驱动程序应请求足够的页映射，以减少到可接受的级别的资源不足的可能性。

如果微型端口驱动程序的策略将缓冲最多 50 个毫秒为单位的数据，例如，读取和写入指针之间记住此限制表示您的驱动程序将会累积，但它不会也不应表示的数据的最长应用驱动程序的流的延迟时间的比例。 您的驱动程序应设计为将其延迟越小越好。 微型端口驱动程序时的微型端口驱动程序开始播放新流之前获取其初始组映射，可以继续请求的映射，直到它达到其缓冲区限制 （在此示例中为 50 毫秒），或没有更多映射将立即可用。 在后一种情况下，但是，微型端口驱动程序必须不等待，直到详细映射变得可用之前开始播放流。 相反，该驱动程序将立即开始播放已获得的映射。 更高版本，如有多个映射时，该驱动程序可以继续获取其他映射，直到它达到了缓冲区大小限制或没有多个映射都可以立即使用。

一般情况下，应设计 WavePci 设备的 DMA 硬件直接访问存储在任意字节对齐的和跨非连续页的物理内存之间的边界的音频帧。 如果有要求映射为整数个音频帧的设备，它支持的音频格式类型中限制该设备。 当然，具有此限制的设备仍应能够处理的音频帧大小是 2 的幂。

例如，具有四个通道和 16 位样本大小的设备需要的音频帧大小为 8 个字节。 整音频帧数适合整齐地页 （或任何其他 8 个字节的倍数的分配帧大小）。 但是，对于具有 16 位样本的 5.1 通道流，音频帧大小为 12 个字节，并且一定超过单个页面的大小的流包含音频跨页边界的帧。 (在图[批筛选器](wave-filters.md)说明这一问题。)不能处理任意字节对齐方式和任意字节长度映射的硬件必须依赖于驱动程序来执行会降低性能的中间副本。

Ac97 示例适配器驱动程序中 Microsoft Windows Driver Kit (WDK) 实现[ **GetAllocatorFraming** ](https://msdn.microsoft.com/library/windows/hardware/ff536726)方法。 微型端口驱动程序使用此方法进行通信其首选的帧分配大小。 在 Windows 2000 和 Windows Me 中，端口驱动程序将调用此方法时，才[拆分器系统驱动程序](kernel-mode-wdm-audio-components.md#splitter_system_driver)(Splitter.sys) 实例化上述输出插针。 在 Windows XP 及更高版本，端口驱动程序的输入流也调用此方法。 请记住，可能会选择 SysAudio 帧分配大小决定时，忽略微型端口驱动程序的首选项。

 

 




