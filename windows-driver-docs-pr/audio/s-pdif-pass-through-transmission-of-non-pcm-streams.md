---
title: 非 PCM 流的 S/PDIF 直通传输
description: 非 PCM 流的 S/PDIF 直通传输
ms.assetid: c06b880e-20d1-417b-9868-a4fb3b418dbf
keywords:
- S/PDIF 传递 WDK 音频
- AC-3-over-S/PDIF 格式 WDK 音频
- 音频非 PCM 格式 WDK
- 非 PCM 音频格式 WDK、 S/PDIF
- WMA Pro WDK 音频
- Ac-3 WDK 音频
- 索尼/菲利普数字接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01e38c1e16935a44861547f95eb5eb385d79c1d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328654"
---
# <a name="spdif-pass-through-transmission-of-non-pcm-streams"></a>非 PCM 流的 S/PDIF 直通传输


## <span id="s_pdif_pass_through_transmission_of_non_pcm_streams"></span><span id="S_PDIF_PASS_THROUGH_TRANSMISSION_OF_NON_PCM_STREAMS"></span>


索尼/菲利普数字接口 (S/PDIF) 格式定义主要用于传输 PCM 音频数据，但它可以轻松地进行适配以便传输非 PCM 数据。 S/PDIF 传递传输的原则是，非 PCM 数据流可以通过 S/PDIF 链接，就好像它是 PCM 流。 直通传输不需要的 S/PDIF 发送和接收端口以了解非 PCM 流的编码。

WMA Pro 和 ac-3 这两种传输称作同步框架的单位的数字音频流的压缩非 PCM 格式。 每个同步框架包含其自己的标头，并且可以独立于流中的其他同步帧解码。 例如，48 kHz 采样率，WMA Pro 同步框架包含数据不足，无法播放 2048年计时周期的示例时钟 （42.67 毫秒为单位）。 在此相同的速率，ac-3 同步框架包含足够的数据 1536年计时周期 （32 毫秒为单位）。

48 kHz 采样率，5.1 通道 WMA Pro 同步框架永远不超过 8192 个字节，这是字节数占用 2048年立体声 （两个通道） 的 16 位 PCM 示例。 同样，5.1 通道 ac-3 同步框架永远不会超过 6144 字节，这是通过 1536年立体声，16 位 PCM 样本已被占用的字节数。 （此规则的例外情况，但这些类型的 ac-3 同步帧是非常少见的不能通过 S/PDIF 传输，可以此处忽略。）

在通过通过以数字形式的 S/PDIF 链接而无需在解码 48 kHz WMA Pro 或 ac-3 音频流，发送和接收端口 S/PDIF 可以视为流相同立体声、 16 位、 48 kHz PCM 流。 指定的 pin，可以使用 WMA Pro-反复-S/PDIF 或 AC-3-over-S/PDIF 流传输的数据范围，波形格式标记本身时，唯一不同的 pin，它通过 S/PDIF 端口 PCM 流传输的数据范围。 有关示例，请参阅中的数据范围声明[指定 WMA Pro 数据范围](specifying-wma-pro-data-ranges.md)。

为了避免通过 S/PDIF 接口比实际时间更快地交付 WMA Pro 压缩的流 (即，可以禁止传递的 43 毫秒为单位的音频不超过 43 毫秒)，音频应用程序必须填充零之前同步具有的 WMA Pro 同步框架框架将占用的字节数为 2048年立体声 PCM 同一个示例。 Ac-3 同步框架必须同样进行填充 1536 大小立体声 PCM 示例。

如果你尝试将未填充的 WMA Pro 或 ac-3 同步帧发送到使用 WaveCyclic PortCls 适配器驱动程序，请注意，当端口驱动程序检测到数据资源不足 （因为数据流包含两个通道未压缩的流相比更少的字节），它将填充具有静默的循环缓冲区。 非 PCM 流解码器会解释这些段 silence、 PCM，而非 PCM 格式中的问题。

下图显示了 S/PDIF 传递传输的一个示例应用程序。

![说明 s/pdif 传递传输的关系图](images/passthru.png)

该图显示了连接到外部 PC 音频/视频 (A / V) 通过同轴电缆连接的接收方。 电缆将 PC 的音频设备上的 S/PDIF 输出端口连接到 S/PDIF 输入端口上为 A / V 接收方。

在该图的左侧边缘，音频应用程序将从 WMA Pro 音频流式传输到 8192 字节缓冲区的开头插入同步框架。 （仅用于易用性图使用此缓冲区大小。 在实践中，缓冲区大小为 4096 个字节或 10240 字节数，例如，可能会改用。）应用程序填充了零缓冲区中的任何剩余空间。 音频驱动程序，就好像它们是 8192 个字节的 PCM 数据缓冲区的内容传输的 S/PDIF 输出端口。

同样，S/PDIF 输入端口上一个 / V 接收方会接收流，就好像它是 8192 个字节的 PCM 数据。 将数据加载到输入缓冲区，它在此示例中还具有 8192 字节的大小。 解码器从输入缓冲区中提取 WMA Pro 同步框架、 解码同步框架为 5.1 声道的音频流，并在上图中的右边缘播放环绕扬声器通过流。

若要使连接另一端知道音频流中的非 PCM 格式的解码器，音频驱动程序应设置 /AUDIO 位 S/PDIF 收发器。 解码器以确定是否非 PCM 格式编码的数据流的 S/PDIF 通道状态块中读取此位。 设置此位是特殊的驱动程序执行操作以容纳的非 PCM 流所需的唯一内容。 每个其他方式，驱动程序会将该流，就好像它包含 PCM 数据。

多个使用者设备支持 S/PDIF 传递传输，但其他数字接口，如 USB 和 1394年还可适应于数字传递到外部音频解码器非 PCM 数据传输。

Dolby Laboratories 1992 年引入 ac-3 （杜比数字） 的压缩音频格式。 第一个使用者 A / V 接收方通过 S/PDIF 支持 ac-3 大约 1997 年推出。 在 2003年中变为可用版本的 Microsoft Windows Media 9 系列技术软件支持 WMA Pro 音频流格式。 A / V 接收方支持 WMA Pro-反复-S/PDIF 2003 中引入了。

在 Windows XP 及更高版本，waveOut、 DirectSound 和 DirectShow Api 支持非 PCM 格式。 DirectSound 和 waveOut Api 中的驱动程序公开任何 PCM 或非 PCM 格式是自动提供给这些 Api 的客户端的方式实现。

 

 




