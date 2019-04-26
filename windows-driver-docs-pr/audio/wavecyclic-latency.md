---
title: WaveCyclic 延迟
description: WaveCyclic 延迟
ms.assetid: 6de639c6-ddd5-4013-8d67-00731c328f47
keywords:
- WaveCyclic 延迟 WDK 音频
- 静默间隔 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0642b2ce576a7b98432dd28466d2b4a20536077e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328499"
---
# <a name="wavecyclic-latency"></a>WaveCyclic 延迟


## <span id="wavecyclic_latency"></span><span id="WAVECYCLIC_LATENCY"></span>


如果 WaveCyclic 微型端口驱动程序提供了硬件混合的音频播放流，DirectSound 将提交到 WaveCyclic 端口驱动程序包含在一个循环缓冲区中的整个 DirectSound 批流 IRP。 WaveCyclic 端口驱动程序接收 IRP，批数据--逐一馈入您的驱动程序公开的 DMA 缓冲区。 WaveCyclic 尝试保留大约 40 毫秒之前读取指针的 DMA 缓冲区写入指针。 即使您的驱动程序执行与 DirectSound 混合的硬件，它有望获得约 40 个毫秒为单位的额外数据 DMA 缓冲区中。

WaveCyclic 端口驱动程序会尝试以累计的循环缓冲区中的数据最多 40 毫秒数的这一事实并不意味着，WaveCyclic 端口驱动程序会增加 40 毫秒为单位的流的延迟时间。 事实上，端口驱动程序添加很少的延迟。 新的流只是开始播放，而端口驱动程序在写入到循环缓冲区开头的初始数据之前，端口驱动程序将继续编写，直到没有更多数据可用或在缓冲区中包含的数据完整 40 毫秒。 但是，如果低于此量数据立即可用，端口驱动程序不会强制等待的微型端口驱动程序。 相反，它允许微型端口驱动程序，若要开始立即播放已缓冲的数据。 更高版本，因为更多数据可用时，端口驱动程序将继续的写入到缓冲区，直到没有更多数据可用或数据量的数据缓冲之间读取和写入指针达到 40 毫秒为单位。

一段后的近资源不足，KMixer 流可以包含无声段间隔。 如果 WaveCyclic 已收到来自 KMixer 维护 30，而不是四十毫秒为单位的 DMA 缓冲区中的额外数据的足够的波形数据，WaveCyclic 开始写入的有效数据结束后从 KMixer DMA 缓冲区静默。 此策略可确保如果资源不足发生并且对于设备读取超过有效的数据的结尾，音频设备呈现无声段而不是陈旧或未初始化的数据。

写入 DMA 缓冲区静默量保持相当小，和如果 KMixer 未成功之前说出 silence 起提供 WaveCyclic 端口驱动程序使用其他数据，该数据将覆盖缓冲区中的静默。 缺少的资源不足的情况下，音频设备接收混合数据而无需强制无声段间隔持续的流。 调试您的驱动程序时，但是，可能会看到微型端口驱动程序[ **IMiniportWaveCyclicStream::Silence** ](https://msdn.microsoft.com/library/windows/hardware/ff536721)即使未耗尽音频输出程序被调用方法。

 

 




