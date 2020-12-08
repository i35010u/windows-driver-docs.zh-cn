---
title: 非 PCM 流的 S/PDIF 直通传输
description: 非 PCM 流的 S/PDIF 直通传输
keywords:
- S/PDIF 传递 WDK 音频
- AC-3-S/PDIF 格式 WDK 音频
- 音频非 PCM 格式 WDK
- 非 PCM 音频格式 WDK，S/PDIF
- WMA Pro WDK 音频
- AC 3 WDK 音频
- 索尼/Philips 数字接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6ef6e2a55e27e1c7fec514d339c8e39e4014891
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800695"
---
# <a name="spdif-pass-through-transmission-of-non-pcm-streams"></a>非 PCM 流的 S/PDIF 直通传输


## <span id="s_pdif_pass_through_transmission_of_non_pcm_streams"></span><span id="S_PDIF_PASS_THROUGH_TRANSMISSION_OF_NON_PCM_STREAMS"></span>


索尼/Philips 数字接口 (S/PDIF) 格式主要用于传输 PCM 音频数据，但可以轻松地将其调整为传输非 PCM 数据。 S/PDIF 传递传输的原则是，非 PCM 数据流可以通过 S/PDIF 链接，就像它是一个 PCM 流一样。 传递传输不需要使用 S/PDIF 发送端口和接收端口来了解非 PCM 流的编码。

WMA Pro 和 AC 3 都是压缩的非 PCM 格式，可将数字音频流以称为同步帧的单位传输。 每个同步帧都包含其自身的标头，并且可以独立于流中的其他同步帧进行解码。 例如，在 48-kHz 采样速率下，WMA Pro 同步帧包含的数据足以播放样本时钟的2048刻度 (42.67 毫秒) 。 按照相同的速度，AC'97 同步帧包含1536刻度 (32 毫秒) 的足够数据。

在 48-kHz 采样速率下，5.1-通道 WMA Pro 同步帧从不超过8192字节，这是2048立体声 (两通道) 16 位 PCM 示例占用的字节数。 同样，5.1 信道 AC 3 同步帧从不超过6144字节，这是1536立体声，16位 PCM 示例占用的字节数。  (存在此规则的例外情况，但这些类型的 AC 3 同步帧非常罕见，无法通过 S/PDIF 传输，可以在此处忽略。 ) 

在未解码的情况下，如果 48-kHz WMA Pro 或 AC 3 音频流通过数字形式的 S/PDIF 链接，则 S/PDIF 发送端口和接收端口可以将流视为与立体声、16位、48-kHz 的流相同。 当为可以传输 WMA Pro-over S/PDIF 或 AC 3 S/PDIF 流的 pin 指定数据范围时，波形格式标记本身是唯一不同于通过 S/PDIF 端口传输 PCM 流的 pin 的数据范围的内容。 有关示例，请参阅 [指定 WMA Pro 数据范围](specifying-wma-pro-data-ranges.md)中的数据范围声明。

为了避免与实时 (相比，在 S/PDIF 接口上传递 WMA Pro 压缩流的速度更快，因此，若要在不到43毫秒的时间内避免交付43毫秒的音频) ，则音频应用程序必须将 WMA Pro 同步帧填充为零，直到同步帧占用与2048立体声 PCM 示例相同的字节数。 AC 3 同步帧必须与1536立体声 PCM 样本的大小相同。

如果尝试将未填充 WMA Pro 或 AC 3 同步帧发送到使用 WaveCyclic 的 PortCls 适配器驱动程序，请注意，当端口驱动程序感知数据不足时 (因为数据流包含的字节数少于两个未压缩的流) ，它将使用无声填充循环缓冲区。 非 PCM 流解码器将在解释这些无声期间（而不是使用非 PCM 格式）出现问题。

下图显示了一个示例应用程序的 S/PDIF 传递传输。

![说明 s/pdif 传递传输的示意图](images/passthru.png)

此图显示了通过同轴电缆连接到外部音频/视频 (A/V) 接收器的 PC。 电缆将电脑音频设备上的 S/PDIF 输出端口连接到 A/V 接收器上的 S/PDIF 输入端口。

在该图的左边缘，音频应用程序将来自 WMA Pro 音频流的同步帧插入8192字节缓冲区的开头。  (此缓冲区大小只是为了便于说明。 例如，可能会改用4096字节或10240字节的缓冲区大小。 ) 应用程序使用零填充缓冲区中的剩余空间。 音频驱动程序会将 S/PDIF 输出端口用于传输缓冲区的内容，就像它们是8192字节的 PCM 数据一样。

同样，A/V 接收器上的 S/PDIF 输入端口接收流，就像它是8192字节的 PCM 数据一样。 它将数据加载到输入缓冲区中，在此示例中，该数据的大小也为8192字节。 解码器从输入缓冲区中提取 WMA Pro 同步帧，将同步帧解码为5.1 通道音频流，并通过图右边缘上的环绕扬声器播放流。

若要使该连接的另一端上的解码器知道音频流采用非 PCM 格式，则音频驱动程序应设置 S/PDIF 收发器上的/AUDIO 位。 解码器从 S/PDIF 通道状态块读取此位，以确定数据流是否以非 PCM 格式进行编码。 设置此位是驱动程序为容纳非 PCM 流而需要执行的唯一特殊操作。 在其他任何情况下，驱动程序都会将流视为包含 PCM 数据。

许多消费者设备支持 S/PDIF 直通传输，但其他数字接口（如 USB 和1394）也可用于对非 PCM 数据到外部音频解码器的数字直通传输进行改编。

杜比实验室在1992中引入了 AC 3 (杜比数字) 压缩音频格式。 如果第一个使用者 A/V 接收方支持通过 S/PDIF 的 AC-3，则会在大约1997中提供。 在2003中发布了 Microsoft Windows Media 9 系列技术后，就可以使用 WMA Pro 音频流格式的软件支持。 支持在2003中引入的支持 WMA Pro/PDIF 的/V 接收器。

在 Windows XP 和更高版本中，waveOut、DirectSound 和 DirectShow Api 支持非 PCM 格式。 DirectSound 和 waveOut Api 以这样一种方式实现：驱动程序公开的任何 PCM 或非 PCM 格式自动对这些 Api 的客户端可用。

 

 




