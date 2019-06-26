---
title: 音频位置属性
description: 音频位置属性
ms.assetid: 893fea84-9136-4107-96d2-8a4e2ab7bd2a
keywords:
- 播放位置 WDK 音频
- 记录位置 WDK 音频
- 音频属性 WDK，流中的位置
- WDM 音频属性 WDK，流中的位置
- 读取位置 WDK 音频
- 编写位置 WDK 音频
- 循环的客户端缓冲区 WDK 音频
- nonlooped 客户端缓冲区 WDK 音频
- 客户端缓冲区 WDK 音频
- 位置 WDK 音频进行流式处理
- 位置属性 WDK 音频
- 捕获位置 WDK 音频进行流式处理
- 端口驱动程序 WDK 音频，position 属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e84e529ff08ec81a265cfad712276f314c04ba19
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355680"
---
# <a name="audio-position-property"></a>音频位置属性


音频驱动程序的客户端使用[ **KSPROPERTY\_音频\_位置**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-position)属性来获取和设置中的音频流的当前位置。 属性使用[ **KSAUDIO\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_position)结构来描述当前的位置。 该结构包含两个成员：**PlayOffset**并**WriteOffset**。

**PlayOffset**并**WriteOffset**成员定义的客户端缓冲区的当前保留以供的音频设备的专用区域的边界。 客户端必须假定，设备可能当前正在访问任何在此区域中包含的数据。 因此，客户端必须访问仅中的部分缓冲区不在此区域。 根据流前进移动区域的边界。

如果客户端缓冲区闭合 (也就是说，流类型是[ **KSINTERFACE\_标准\_LOOPED\_流式处理**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-looped-streaming))， **PlayOffset**并**WriteOffset**是缓冲区的相对偏移量。 也就是说，它们被指定为从循环的客户端缓冲区开头的字节偏移量。 当任何一个偏移量递增到缓冲区的末尾时，它会绕到缓冲区的起始位置。 （开始的缓冲区开始处的偏移量为零）。因此，既不偏移量曾经超出缓冲区大小。

如果客户端缓冲区 nonlooped (也就是说，流类型是[ **KSINTERFACE\_标准\_流式处理**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-streaming))， **PlayOffset**和**WriteOffset**是流的相对偏移量。 也就是说，它们被指定为字节偏移量从流的开始。 这些偏移量可以认为的偏移量到包含整个流并位于连续的从开头到末尾的理想化缓冲区。

在呈现流的情况下**PlayOffset**成员指定的流播放位置并**WriteOffset**成员指定流的写入位置。 下图显示了客户端缓冲区中的播放和写入位置。

![说明的 play 位置和呈现流中的写入位置的关系图](images/playoffset.png)

播放位置是当前正在播放的示例的字节偏移量 （即，则会在数字模拟转换器或 DAC 的输入示例）。 写入位置是超出该客户端可以安全地写入到缓冲区的位置。 流播放时，播放和写入位置移动从左到右在上图中。 客户端的写入操作必须保持领先的写入位置。 此外，如果循环缓冲区，客户端的写入操作必须永远不会取代播放位置。

尽管 WaveCyclic 或 WavePci 端口驱动程序依赖于要跟踪的 play 位置的微型端口驱动程序，但端口驱动程序将跟踪的写入位置。 WaveCyclic 和 WavePci 端口驱动程序更新的写入位置，如下所示：

-   **WaveCyclic**

    每次 WaveCyclic 端口驱动程序调用[ **IDmaChannel::CopyTo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-copyto)若要将新数据块 （从客户端缓冲区） 复制到循环缓冲区中，写入位置，转到的位置 （在客户端缓冲区） 的数据块中的最后一个字节。

-   **WavePci**

    默认情况下，每次 WavePci 微型端口驱动程序调用[ **IPortWavePciStream::GetMapping** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-getmapping)以获取新的映射 （客户端缓冲区的一部分） 和调用成功，写入位置前移到新映射中的最后一个字节的位置 （在客户端缓冲区）。

    如果 WavePci 微型端口驱动程序重写默认行为，通过指定偏移量到端口驱动程序的预提取，当前的写入位置始终是等于当前播放位置和预提取偏移量的总和。 有关详细信息，请参阅[预提取偏移量](prefetch-offsets.md)。

在捕获流的情况下**PlayOffset**成员指定的记录位置的流，并**WriteOffset**成员指定读取的流的位置。 下图显示了的记录，并读取客户端缓冲区中的位置。

![关系图阐释的记录位置并读取捕获流中的位置](images/recordoffset.png)

记录位置是示例的最新，若要模拟到数字转换器或 ADC 的输出在闩锁的字节偏移量。 （此位置指定到其中的音频设备的 DMA 引擎最终将写入示例的缓冲区位置。）读取的位置是超出该客户端安全地无法从缓冲区读取的位置。 作为流进行录制，读取和记录的位置继续学习从左到右在上图中。 客户端的读取必须结尾读取的位置。 此外，如果循环缓冲区，客户端的读取必须保持领先的记录位置。

尽管 WaveCyclic 或 WavePci 端口驱动程序依赖于要跟踪的记录位置的微型端口驱动程序，但端口驱动程序将跟踪的读取的位置。 WaveCyclic 和 WavePci 端口驱动程序更新读取的位置，如下所示：

-   **WaveCyclic**

    每次 WaveCyclic 端口驱动程序调用[ **IDmaChannel::CopyFrom** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-copyfrom)将新数据块从循环缓冲区复制 （到客户端缓冲区），读取的位置，转到的位置 （在客户端缓冲区） 的数据块中的最后一个字节。

-   **WavePci**

    每次 WavePci 微型端口驱动程序调用[ **IPortWavePciStream::ReleaseMapping** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-releasemapping)若要释放的以前获取的映射 （客户端缓冲区的一部分），读取的位置，转到（在客户端缓冲区） 的已发布的映射中的最后一个字节的位置。

微型端口驱动程序不需要实现处理程序例程 KSPROPERTY\_音频\_位置属性请求。 相反，WaveCyclic 和 WavePci 端口驱动程序处理这些请求代表微型端口驱动程序。 在处理获取属性请求时，WaveCyclic 或 WavePci 端口驱动程序已具有计算所需的所有信息**WriteOffset**值，但它仍需要从微型端口驱动程序，来计算信息**PlayOffset**值。 若要获取此信息，端口驱动程序调用微型端口驱动程序[ **IMiniportWaveCyclicStream::GetPosition** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-getposition)或[ **IMiniportWavePciStream::GetPosition** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-getposition)方法。

为呈现的流**GetPosition**方法检索的 play 位置的示例通过 DAC 当前正在播放的字节偏移量。 为捕获的流**GetPosition**方法检索的记录的位置的最新的示例由 ADC 捕获的字节偏移量。

请注意，偏移量的值来检索**GetPosition**调用是对应于当前传输通过演讲者 jack 的信号的 play 位置或当前正在将信号与相对应的记录位置通过麦克风 jack 接收。 它不是 DMA 位置。 （DMA 位置是示例的音频设备中的 DMA 引擎当前正在转移到或从 DMA 缓冲区的字节偏移量。）

一些音频硬件包含位置注册，以跟踪的示例中的每个 DAC 或 ADC，当前的字节偏移量，在这种情况下**GetPosition**方法只需检索位置注册的内容适当的流。 其他音频硬件只能提供驱动程序通过 DMA 位置，在这种情况下**GetPosition**方法必须考虑当前 DMA 位置提供的示例中的 DAC 或 ADC 的字节偏移量的最佳估计和设备的内部缓存延迟。

尽管 WaveCyclic 或 WavePci 端口驱动程序中的属性处理程序必须区分循环和 nonlooped 缓冲区，以确定是否提供流相对路径或相对于缓冲区的字节偏移量，此详细信息 (即，在循环缓冲区是否或nonlooped) 对微型端口驱动程序是透明的。

**IMiniportWaveCyclicStream::GetPosition**方法将始终报告或记录的位置，而不考虑客户端缓冲区是否循环或 nonlooped 缓冲区相对播放。 闭合的客户端缓冲区，如果属性处理程序会将转换报告的微型端口驱动程序，可以循环缓冲区，为到客户端缓冲区，该处理程序然后将写入偏移量表示为一个偏移的缓冲区的相对位置**PlayOffset**成员。 如果客户端缓冲区 nonlooped，属性处理程序之前将转换缓冲区相对 play 位置到流相对 play 位置写入到**PlayOffset**成员。

**IMiniportWavePciStream::GetPosition**方法将始终报告而不考虑客户端缓冲区是否循环或 nonlooped 记录位置或流相对播放。 闭合的客户端缓冲区，如果属性处理程序之前将转换的流相对 play 位置将其置于缓冲区相对 play （表示为某一偏移量到客户端缓冲区） 写入到**PlayOffset**中的成员KSAUDIO\_属性请求中的位置结构。 如果客户端缓冲区 nonlooped，属性处理程序写入到的流相对位置**PlayOffset**成员。

播放或记录的位置是流的零紧跟其后初始化。 过渡到 KSSTATE\_停止状态 (请参阅[ **KSSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksstate)) 位置重置为零。 从 KSSTATE 的转换时暂停流\_运行到 KSSTATE\_暂停或 KSSTATE\_采集位置会冻结。 它取消冻结时流转换从 KSSTATE\_暂停或 KSSTATE\_回 KSSTATE ACQUIRE\_运行。

有关示例的实现**GetPosition**方法 WaveCyclic 和 WavePci 微型端口驱动程序，请参阅示例音频驱动程序 Windows Driver Kit (WDK) 中。

 

 




