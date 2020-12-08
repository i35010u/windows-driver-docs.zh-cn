---
title: WaveCyclic 延迟
description: WaveCyclic 延迟
keywords:
- WaveCyclic 延迟 WDK 音频
- 静默间隔 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d36a507dfa4956f4b3aaebccd599b27b26019abc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802093"
---
# <a name="wavecyclic-latency"></a>WaveCyclic 延迟


## <span id="wavecyclic_latency"></span><span id="WAVECYCLIC_LATENCY"></span>


如果你的 WaveCyclic 微型端口驱动程序提供了音频播放流的硬件混合，则 DirectSound 会将 IRP 提交到 WaveCyclic 端口驱动程序，该驱动程序包含一个循环缓冲区中的整个 DirectSound 波形流。 WaveCyclic 端口驱动程序接收 IRP，并将波形数据逐个写入驱动程序公开的 DMA 缓冲区。 WaveCyclic 尝试使 DMA 缓冲区的写指针大约在读取指针之前40毫秒。 即使驱动程序与 DirectSound 进行硬件混合，它也可能会预计在 DMA 缓冲区中有大约40毫秒的额外数据。

WaveCyclic 端口驱动程序尝试在循环缓冲区中累积最多40毫秒的数据并不意味着 WaveCyclic 端口驱动程序将40毫秒添加到流的滞后时间。 事实上，端口驱动程序会增加极少的延迟。 在新流开始播放前，如果端口驱动程序仍将初始数据写入到循环缓冲区的开头，则端口驱动程序将继续写入，直到没有更多数据可用，或者缓冲区包含完整的40毫秒的数据。 但是，如果此数量的数据立即可用，端口驱动程序将不会强制等待微型端口驱动程序。 相反，它允许微型端口驱动程序立即开始播放已缓冲的数据。 稍后，当有更多数据可用时，端口驱动程序会继续将数据写入缓冲区，直到没有更多的数据可用，或者读和写指针之间缓冲的数据量达到40毫秒。

在接近不足的一段时间后，KMixer 流可以包含无声间隔。 如果 WaveCyclic 只接收到来自 KMixer 的足够波形数据来维护 DMA 缓冲区中的三十个额外数据而不是40毫秒，则 WaveCyclic 将在来自 KMixer 的有效数据结束后，开始将无声写入 DMA 缓冲区。 此策略可确保如果发生了不足并且设备读取了有效数据的末尾，则音频设备将呈现无声，而不是陈旧或未初始化的数据。

写入 DMA 缓冲区的静默量会保持相当小，如果 KMixer 在 WaveCyclic 端口驱动程序在无声之前为其他数据提供了成功，则该数据会在缓冲区中覆盖无声。 如果没有任何资源，则音频设备将接收混合数据的连续流，而不会有强制无声的间隔。 但在调试驱动程序时，可能会看到微型端口驱动程序的 [**IMiniportWaveCyclicStream：：无声**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-silence) 方法正在调用，即使音频呈现器不是从而使。

 

