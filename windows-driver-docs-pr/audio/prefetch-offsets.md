---
title: 预提取偏移量
description: 预提取偏移量
ms.assetid: 92a0163f-29b1-4e15-88ab-67e1097d015e
keywords:
- 硬件加速 WDK DirectSound，预提取的偏移量
- 预提取的偏移量 WDK 音频
- 写入光标的偏移量 WDK 音频
- 游标偏移量 WDK 音频播放
- 偏移量 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d15ec687ae4cbec93025efc99e9df5862a0fb7b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328756"
---
# <a name="prefetch-offsets"></a>预提取偏移量


## <span id="prefetch_offsets"></span><span id="PREFETCH_OFFSETS"></span>


WavePci 微型端口驱动程序调用[ **IPreFetchOffset::SetPreFetchOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff536952)方法，以指定的预提取偏移量的硬件加速 DirectSound 输出流。 此偏移量是将写入光标从 play 光标音频设备的硬件缓冲区中分离出来的数据的字节数。 写入光标指定在其中 DirectSound 应用程序可以安全地编写的下一步的声音样本的缓冲区位置。 Play 游标指定当前正在播放的音频设备的声音样本的缓冲区位置。

DirectSound 查询 WavePci 端口驱动程序当前播放的位置，并通过发送写入光标[ **KSPROPERTY\_音频\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff537297)属性请求。 此请求的响应，端口驱动程序将获取当前播放位置从微型端口驱动程序通过调用[ **IMiniportWavePciStream::GetPosition**](https://msdn.microsoft.com/library/windows/hardware/ff536727)。 端口驱动程序如何确定写入位置取决于是否[ **SetPreFetchOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff536952)已调用。

默认情况下，端口驱动程序会以请求微型端口驱动程序的最后一个映射定位写入光标。 每次调用[ **IPortWavePciStream::GetMapping**](https://msdn.microsoft.com/library/windows/hardware/ff536909)，默认预提取偏移量的增长。 如果 WavePci 微型端口驱动程序获取了大量的映射，则默认偏移量可以变得很大。

调用[ **SetPreFetchOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff536952)重写默认值。 在此调用，端口驱动程序通过将指定的预提取偏移量添加到播放位置 （考虑 DirectSound 缓冲区末尾自动换行） 计算的写入位置。

微型端口驱动程序可能为几个原因分配大量的映射。 一个是减少系统处理器上的音频操作的开销。 使用多个映射，该驱动程序需要更少的中断保护音频设备持续提供数据。 另一个原因是，分配多个映射减少可能性音频播放将发生故障时的运转情况极差的设备驱动程序占用系统短时间内。

具有较大的预提取的偏移量的一个问题是某些 DirectSound 应用程序可以播放的相对位置有关困惑并写入光标。 在 Windows 95/98 中，音频 Vxd 维护相对较小的预提取的偏移量，和如果偏移量大于他们期望，DirectSound 为这些操作系统编写的应用程序可能无法正常运行。

例如，应用程序可能会划分为 DirectSound 缓冲区上半部分和下半部分，然后"ping pong"应用程序和设备之间的两个部分。 当写入光标首次进入缓冲区的上限或下限的一半时，它将一半缓冲区的积累的数据写入到缓冲区的一半。 此方案假定 play 游标将始终置于另一半的缓冲区，不会被写入到的一半。 请注意，此假设不正确，是否预提取偏移量超出了缓冲区大小的一半。 这种情况下，当写入光标达到 DirectSound 缓冲区的末尾，并包装到缓冲区的开头，它将为 play 游标缓冲区的相同部分。 当应用程序将一半缓冲区的积累的数据写入新的写入光标位置时，它最终覆盖 play 光标位置，然后再销毁未尚未播放的数据。

尽管此类故障可以肯定怪应用程序本身，WavePci 微型端口驱动程序可以消除故障模式，只需通过调用[ **SetPreFetchOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff536952)设置预提取为较小值的偏移量。

将预提取偏移量设置为较小的值将生成的写入光标更接近移到 play 游标。 您应设置为您的硬件的先进先出大小的预提取偏移量。 典型的预提取偏移量是大约 64 示例，具体取决于 DMA 引擎的硬件设计。

为了保持某些较旧的 DirectSound 应用程序兼容，DirectSound 将当前由 10 毫秒补充硬件加速的 pin 的写入游标。 请注意，可能会在将来更改的填充量。

有关管理写入游标和 play 游标在驱动程序级别的其他信息，请参阅[音频 Position 属性](audio-position-property.md)。

 

 




