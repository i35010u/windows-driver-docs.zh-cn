---
title: 指定拓扑
description: 指定拓扑
ms.assetid: 265cbd87-d40f-4ead-ba6e-a1cef51baf95
keywords:
- WDM 音频驱动程序 WDK、 拓扑
- 音频驱动程序 WDK、 拓扑
- 拓扑 WDK 音频
- KS 拓扑 WDK 音频
- 内核流拓扑 WDK 音频
- PortCls WDK 音频，拓扑
- 端口驱动程序 WDK 音频，拓扑
- 拓扑端口驱动程序 WDK 音频
- 音频混合拓扑 WDK 音频
- KS pin WDK 音频，拓扑
- KS 筛选器 WDK 音频，拓扑
- 筛选器 WDK 音频 KS
- pin WDK 音频 KS
- 音频适配器 WDK、 拓扑
- 桥 pin WDK 音频
- KS 属性 WDK 音频
- 属性请求 WDK 音频
- PCM wave 输出 WDK 音频
- S/PDIF 传递 WDK 音频
- 混合使用音频 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a50bb863d0cbee614d40fd6f5cc14ac745d33fe1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354308"
---
# <a name="specifying-the-topology"></a>指定拓扑


硬件供应商决定要编写批和 MIDI 设备的微型端口驱动程序后下, 一步是表示内核流式处理 (KS) 的这些设备的拓扑。 KS 拓扑包含的一组描述音频或 MIDI 流按照流过每个设备的数据路径的数据结构。 通过此拓扑中，该驱动程序公开的每个路径沿着控件节点 （例如，音量控制）。 通常情况下，应用程序使用 Windows 多媒体 mixer*Xxx*函数，以了解拓扑枚举的每个路径上的节点序列。 例如，在发现的卷级别控制节点之后, 应用程序可以设置音量级别该节点上。 有关 Windows 多媒体的详细信息，请参阅 Microsoft Windows SDK 文档。 详细了解通过 mixer KS 拓扑的表示形式*Xxx*函数，请参阅[音频 Mixer API 转换到内核流式处理拓扑](kernel-streaming-topology-to-audio-mixer-api-translation.md)。

PortCls 提供了六个端口驱动程序：WavePci、 WaveCyclic、 WaveRT、 MIDI、 Dmu 和拓扑。 （WaveRT 自 Windows Vista 和是建议的方法。）拓扑端口驱动程序控制混合在一起使用从批和 MIDI 设备呈现流的音频适配器电路的部分。 它还可以控制从输入插孔捕获流的所选内容。 尽管它有点令人误解的名称，拓扑端口驱动程序不包含所有音频适配器的拓扑，尽管通常它包含它有很大一部分。 其他端口驱动程序提供适配器的拓扑的其余的部分。

每个端口驱动程序与相应的微型端口驱动程序，向窗体配对[KS 筛选器](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-filters)，表示音频的适配器上的特定设备 （批、 MIDI 或 mixer） 下, 表中所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">筛选器类型</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Wave<em>Xxx</em>筛选器</p></td>
<td align="left"><p>表示用于将 wave 输出流转换为模拟音频信号或用于将模拟音频信号转换到的批输入流的波形设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MIDI 或 Dmu 筛选器</p></td>
<td align="left"><p>表示播放或捕获 MIDI 流的 MIDI 设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>拓扑筛选器</p></td>
<td align="left"><p>表示适配器的混音器电路。</p></td>
</tr>
</tbody>
</table>

 

微型端口驱动程序实现筛选器的特定于设备的功能，包括设备包含适配器拓扑的一部分的定义。 端口驱动程序负责的普通筛选器操作，包括与操作系统，每种类型的筛选器的通信。

每个筛选器具有一个或多个[KS pin](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-pins)作为要进入和离开该筛选器的音频数据的数据流的路径。 通常情况下，拓扑筛选器上的针上批，MIDI，绑定到球瓶和 Dmu 的筛选器通过适配器电路中的硬编码连接。 这些筛选器和及其互连组合在一起形成包含适配器的拓扑的 KS 筛选器关系图。

下图显示了示例音频适配器的拓扑。

![说明的音频适配器拓扑关系图](images/topoexample.png)

在上图中，最高级别的拓扑的 MIDI，批之间的连接由构成*Xxx*，和拓扑筛选器。 此外，每个筛选器具有其自身内部拓扑中，其中包括通过筛选器和每个路径沿着控制节点的数据路径。 下表中所示，节点进行标记。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Label</th>
<th align="left">描述</th>
<th align="left">KS 节点类型的 GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>合成器</p></td>
<td align="left"><p>合成器节点</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer" data-raw-source="[&lt;strong&gt;KSNODETYPE_SYNTHESIZER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer)"><strong>KSNODETYPE_SYNTHESIZER</strong></a></td>
</tr>
<tr class="even">
<td align="left"><p>DAC</p></td>
<td align="left"><p>数字音频转换器节点</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac" data-raw-source="[&lt;strong&gt;KSNODETYPE_DAC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac)"><strong>KSNODETYPE_DAC</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p>ADC</p></td>
<td align="left"><p>模拟到数字转换器节点</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-adc" data-raw-source="[&lt;strong&gt;KSNODETYPE_ADC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-adc)"><strong>KSNODETYPE_ADC</strong></a></td>
</tr>
<tr class="even">
<td align="left"><p>Volume</p></td>
<td align="left"><p>卷级别控制节点</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume" data-raw-source="[&lt;strong&gt;KSNODETYPE_VOLUME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)"><strong>KSNODETYPE_VOLUME</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p>Mute</p></td>
<td align="left"><p>静音控制节点</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mute" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUTE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mute)"><strong>KSNODETYPE_MUTE</strong></a></td>
</tr>
<tr class="even">
<td align="left"><p>Sum</p></td>
<td align="left"><p>总和节点</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum" data-raw-source="[&lt;strong&gt;KSNODETYPE_SUM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum)"><strong>KSNODETYPE_SUM</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p>MUX</p></td>
<td align="left"><p>多路复用器节点</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux)"><strong>KSNODETYPE_MUX</strong></a></td>
</tr>
</tbody>
</table>

 

在上图中，左侧和右侧的音频的适配器上的针表示通过哪些数据的流输入适配器从系统总线或从适配器输入系统总线的逻辑连接 （不是物理连接）。 这些引脚以逻辑方式连接到源和接收器插针上其他 （未显示） 的筛选器外部的适配器。 通常情况下，这些筛选器是软件模块，与适配器拓扑一起形成更大的筛选器图形的拓扑可以探讨了应用程序通过 mixer*Xxx*函数。 例如，在上图中标记为"PCM 批 Out"pin 是以逻辑方式连接到 Windows 中的用户模式音频引擎。 通过系统总线，通过 DMA 传输保持这些逻辑连接。

与此相反，拓扑筛选器的左边缘上的针以物理方式连接到瓶 MIDI 和 Wave*Xxx*筛选器。 这些连接硬编码，软件不能更改。

音频适配器右侧桥插针表示系统机箱上的音频插孔。 这些引脚嘿 *桥接 pin* 因为它们桥接 KS 筛选器关系图并与外部环境之间的边界。

筛选器、 pin 和节点通常有的客户端 （内核模式组件或用户模式应用程序） 的音频驱动程序可以访问的属性。 客户端可以发送[KS 属性请求](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)到筛选器、 pin 或节点属性的当前值的查询，或若要更改属性值。 例如，卷级别控制节点具有[ **KSPROPERTY\_音频\_VOLUMELEVEL** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)属性，客户端可以更改通过 KS 属性请求。 总和节点是通常具有任何属性的节点类型的示例。

为简单起见，Wave*Xxx*在上图中的筛选器提供单个插针用于接受来自系统总线的 PCM wave 输出流。 与此相反，某些波形设备 PCM wave 输出为提供多个插针，并且包含在内部混合的流的输入插针的硬件。 这些设备提供硬件加速的应用程序通过接受从应用程序的声音缓冲区播放 PCM 流使用 DirectSound。 若要使用这些引脚的 DirectSound，他们必须提供的其他节点的二维 (2-d) 和三维 (3-D) 处理，如中所述[DirectSound WDM 音频中的硬件加速](directsound-hardware-acceleration-in-wdm-audio.md)。

这种类型的硬件加速支持在 Windows Server 2003、 Windows XP、 Windows 2000 和 Windows Me 98，但它不支持在 Windows Vista 中。 Windows Vista 使较旧的波形设备上无需使用的硬件加速 pin。

在上图中，MIDI，批之间的物理连接*Xxx*，并且拓扑筛选所有传输模拟音频信号。 但是，不同的拓扑设备可能会接受数字输出流中的 MIDI 和波形设备、 数字混合使用它们，并将数字的组合转换为模拟输出信号实现类似的效果。

在上图中的左下角的"非 PCM 批 Out"pin 接受 S/PDIF 传递格式，如 AC-3-over-S/PDIF 或 WMA Pro-反复-S/PDIF 的非 PCM 输出流。 使用以下格式之一，设备只需将压缩的数据传输通过 S/PDIF 链接而无需解码数据。 出于此原因，到在上图中右下角的"S/PDIF Out"插针的数据路径包含没有音量或静音节点。 有关非 PCM 音频格式和 S/PDIF 传递传输的详细信息，请参阅[支持非 PCM 波形格式](supporting-non-pcm-wave-formats.md)。 在标题为的白皮书提供了其他信息*WMA Pro-反复-S/PDIF 格式的音频驱动程序支持*处[音频技术](https://go.microsoft.com/fwlink/p/?linkid=8751)网站。

微型端口驱动程序提供的窗体中的端口驱动程序对其拓扑[ **PCFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcfilter_descriptor)结构。 此结构描述的所有筛选器的插针和节点，并指定的 pin 和节点如何连接到对方。

而不是设计整体化拓扑筛选器，在上图所示的混音器电路中音频的适配器可以将分区到多个拓扑筛选器。 例如，在上图中，驱动器演讲者的数据路径可能会实现为一个拓扑筛选器，并捕获音频数据从输入设备的数据路径可以作为单独的拓扑筛选器实现。 当特定的拓扑筛选器中使用的数据路径将未在使用中时，可以但不能禁用整个适配器关闭电源适配器的该部分。 有关详细信息，请参阅[动态音频子设备](dynamic-audio-subdevices.md)。

 

 




