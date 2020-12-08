---
title: 音频位置属性
description: 音频位置属性
keywords:
- 播放位置 WDK 音频
- 录制位置 WDK 音频
- 音频属性 WDK，流中的位置
- WDM 音频属性 WDK，在流中的位置
- 读取位置 WDK 音频
- 写入位置 WDK 音频
- 循环的客户端缓冲 WDK 音频
- nonlooped 客户端缓冲 WDK 音频
- 客户端缓冲 WDK 音频
- 流位置 WDK 音频
- 位置属性 WDK 音频
- 捕获流位置 WDK 音频
- 端口驱动程序 WDK 音频，位置属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 888b3e82c7f0655dc8a53fe3afd86f3be068a674
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784981"
---
# <a name="audio-position-property"></a>音频位置属性


音频驱动程序的客户端使用 [**KSPROPERTY \_ 音频 \_ 位置**](./ksproperty-audio-position.md) 属性来获取和设置音频流中的当前位置。 属性使用 [**KSAUDIO \_ 位置**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_position) 结构来描述当前位置。 结构包含两个成员： **PlayOffset** 和 **WriteOffset**。

**PlayOffset** 和 **WriteOffset** 成员定义当前为独占使用音频设备而保留的客户端缓冲区区域的边界。 客户端必须假定设备当前正在访问此区域中包含的任何数据。 因此，客户端必须仅访问位于此区域之外的缓冲区部分。 当流前进时，区域的边界会移动。

如果客户端缓冲区具有循环 (也就是说，流类型为 [**KSINTERFACE \_ 标准 \_ 循环 \_ 流式处理**](../stream/ksinterface-standard-looped-streaming.md)) ， **PlayOffset** 和 **WriteOffset** 是缓冲区相对偏移量。 也就是说，它们被指定为从循环客户端缓冲区开始的字节偏移量。 当偏移量增量到缓冲区的末尾时，它将环绕到缓冲区的开头。  (缓冲区开始处的偏移量为零。 ) 因此，两次偏移都不会超出缓冲区大小。

如果客户端缓冲区为 nonlooped (也就是说，流类型为 [**KSINTERFACE \_ STANDARD \_ 流式处理**](../stream/ksinterface-standard-streaming.md)) ， **PlayOffset** 和 **WriteOffset** 是流相对偏移量。 也就是说，它们被指定为从流开头开始的字节偏移量。 可以将这些偏移视为包含整个流的理想化缓冲区的偏移量，并且从开头到结尾是连续的。

对于呈现流， **PlayOffset** 成员指定流的播放位置，而 **WriteOffset** 成员指定流的写入位置。 下图显示了客户端缓冲区中的播放和写入位置。

![说明呈现流中的播放位置和写入位置的关系图](images/playoffset.png)

播放位置是当前正在播放的样本的字节偏移量 (即，在数字到模拟转换器的输入或 DAC) 锁定的示例。 写入位置是客户端可以安全写入缓冲区的位置。 当流播放时，播放和写入位置在上图中从左到右移动。 客户端的写入必须位于写入位置之前。 此外，如果缓冲区是循环的，则客户端的写入永远不能 overtake 播放位置。

尽管 WaveCyclic 或 WavePci 端口驱动程序依赖于微型端口驱动程序来跟踪播放位置，但端口驱动程序仍跟踪写入位置。 WaveCyclic 和 WavePci 端口驱动程序更新写入位置，如下所示：

-   **WaveCyclic**

    每次 WaveCyclic 端口驱动程序调用 [**IDmaChannel：： CopyTo**](/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyto) 以将新数据块复制到 (从客户端缓冲区) 的循环缓冲区时，写入位置会前进到数据块中最后一个字节) 客户端缓冲区中的位置 (。

-   **WavePci**

    默认情况下，每次 WavePci 微型端口驱动程序调用 [**IPortWavePciStream：： GetMapping**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-getmapping) 以获取 (一部分客户端) 缓冲区 (的新映射，并且调用成功后，写入位置会前进到新映射中最后一个字节) 客户端缓冲区中的位置。

    如果 WavePci 微型端口驱动程序通过指定端口驱动程序的预提取偏移量来覆盖默认行为，则当前写入位置始终等于当前播放位置和预提取偏移量之和。 有关详细信息，请参阅 [预提取偏移量](prefetch-offsets.md)。

对于捕获流， **PlayOffset** 成员指定流的记录位置，而 **WriteOffset** 成员指定流的读取位置。 下图显示了客户端缓冲区中的记录和读取位置。

![阐释捕获流中的记录位置和读取位置的关系图](images/recordoffset.png)

记录位置是最新示例的字节偏移量，将在模拟到数字转换器或 ADC 的输出上锁定。  (此位置指定音频设备 DMA 引擎最终写入样本的缓冲区位置。 ) 读取位置是客户端无法安全地从缓冲区中读取的位置。 当流的记录正在进行时，读取和记录位置将从上图中的左到右前进。 客户端的读取必须记录读取位置。 此外，如果缓冲区是循环的，则客户端的读取必须停留在记录位置之前。

尽管 WaveCyclic 或 WavePci 端口驱动程序依赖于微型端口驱动程序来跟踪记录位置，但端口驱动程序仍跟踪读取位置。 WaveCyclic 和 WavePci 端口驱动程序更新读取位置，如下所示：

-   **WaveCyclic**

    每次 WaveCyclic 端口驱动程序调用 [**IDmaChannel：： CopyFrom**](/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyfrom) 将新数据块从循环缓冲区 (复制到客户端缓冲区) 时，读取位置会前进到数据块中最后一个字节) 客户端缓冲区中的位置 (。

-   **WavePci**

    每次 WavePci 微型端口驱动程序调用 [**IPortWavePciStream：： ReleaseMapping**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-releasemapping) 来释放以前获取的映射 (部分客户端缓冲区) 时，读取位置会前进到客户端缓冲区中的位置 (在发布的映射中最后一个字节) 的位置。

微型端口驱动程序无需实现 KSPROPERTY \_ 音频位置属性请求的处理程序例程 \_ 。 相反，WaveCyclic 和 WavePci 端口驱动程序代表微型端口驱动程序处理这些请求。 处理 get 属性请求时，WaveCyclic 或 WavePci 端口驱动程序已经包含计算 **WriteOffset** 值所需的全部信息，但它仍需要来自微型端口驱动程序的信息来计算 **PlayOffset** 值。 为获取此信息，端口驱动程序将调用微型端口驱动程序的 [**IMiniportWaveCyclicStream：： GetPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-getposition) 或 [**IMiniportWavePciStream：： GetPosition**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition) 方法。

对于呈现流， **GetPosition** 方法检索播放位置-当前正在通过 DAC 播放的样本的字节偏移量。 对于捕获流， **GetPosition** 方法将检索记录位置-要由 ADC 捕获的最新示例的字节偏移量。

请注意， **GetPosition** 调用检索的偏移量值是相对于当前通过扬声器插孔传输的信号的播放位置，或是相对于当前通过麦克风插孔接收的信号的记录位置。 它不是 DMA 位置。 DMA 位置 (DMA 位置是音频设备中 DMA 引擎当前正在传输到 DMA 缓冲区或从 DMA 缓冲区传输的字节偏移量。 ) 

某些音频硬件包含位置注册，用于跟踪当前在每个 DAC 或 ADC 中的示例的字节偏移量，在这种情况下， **GetPosition** 方法只检索相应流的位置寄存器的内容。 其他音频硬件只能提供 DMA 位置的驱动程序，在这种情况下， **GetPosition** 方法必须通过考虑当前 DMA 位置和设备内部的缓冲延迟，为 DAC 或 ADC 中样本的字节偏移量提供最佳估计。

尽管 "WaveCyclic" 或 "WavePci" 端口驱动程序中的属性处理程序必须区分循环的和 nonlooped 的缓冲区，以确定是提供流相对还是缓冲区相对字节偏移量，但此详细 (也就是说，缓冲区是循环的还是 nonlooped) 对于微型端口驱动程序是透明的。

无论客户端缓冲区是循环还是 nonlooped， **IMiniportWaveCyclicStream：： GetPosition** 方法都将报告相对于缓冲区的播放或记录位置。 如果客户端缓冲区是循环的，则属性处理程序会将微型端口驱动程序报告的相对于缓冲区的位置（表示为循环缓冲区的偏移量）转换为客户端缓冲区的偏移量，然后处理程序会将其写入 **PlayOffset** 成员。 如果客户端缓冲区是 nonlooped 的，则属性处理程序会将缓冲区相对播放位置转换为流相对播放位置，然后再将其写入 **PlayOffset** 成员。

无论客户端缓冲区是循环还是 nonlooped， **IMiniportWavePciStream：： GetPosition** 方法始终报告与流相关的播放或记录位置。 如果客户端缓冲区是循环的，则属性处理程序会将流相关的播放位置转换为相对于缓冲区的播放位置 (表示为客户端缓冲区) 的偏移量，然后将其写入到属性请求中 KSAUDIO 位置结构中的 **PlayOffset** 成员 \_ 。 如果客户端缓冲区为 nonlooped，则属性处理程序会将流相对位置写入 **PlayOffset** 成员。

在流的初始化后，播放或记录位置立即为零。 转换到 KSSTATE \_ 停止状态 (参阅 [**KSSTATE**](/windows-hardware/drivers/ddi/ks/ne-ks-ksstate)) 将位置重置为零。 当从 KSSTATE \_ 运行到 KSSTATE 暂停或 KSSTATE 获取的转换停止流时 \_ \_ ，位置将冻结。 当流从 KSSTATE \_ 暂停或 KSSTATE \_ 恢复到 KSSTATE 运行时 unfreezes \_ 。

有关 WaveCyclic 和 WavePci 微型端口驱动程序的 **GetPosition** 方法的实现示例，请参阅 Windows 驱动程序工具包 (WDK) 中的示例音频驱动程序。

 

