---
title: 指定拓扑
description: 指定拓扑
ms.assetid: 265cbd87-d40f-4ead-ba6e-a1cef51baf95
keywords:
- WDM 音频驱动程序 WDK，拓扑
- 音频驱动程序 WDK，拓扑
- 拓扑 WDK 音频
- KS 拓扑 WDK 音频
- 内核流拓扑 WDK 音频
- PortCls WDK 音频，拓扑
- 端口驱动程序 WDK 音频，拓扑
- 拓扑端口驱动程序 WDK 音频
- 音频混合拓扑 WDK 音频
- KS 引脚音频、拓扑
- KS 筛选 WDK 音频、拓扑
- 筛选 WDK 音频、KS
- 固定 WDK 音频、KS
- 音频适配器 WDK，拓扑
- 桥接 WDK 音频
- KS 属性 WDK 音频
- 属性请求 WDK 音频
- PCM 波纹输出 WDK 音频
- S/PDIF 传递 WDK 音频
- 混合音频 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 740c5ae43af6d34f40d9d6a9b3b088f4b00b01ae
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102304"
---
# <a name="specifying-the-topology"></a>指定拓扑

硬件供应商确定要为 wave 和 MIDI 设备写入哪些小型小型驱动程序后，下一步是表示这些设备的内核流式处理 (KS) 拓扑。 KS 拓扑包含一组数据结构，这些结构描述音频或 MIDI 流流过每个设备时遵循的数据路径。 在此拓扑中，驱动程序将公开控件节点 (例如，位于每个路径中的音量控制) 。 通常，应用程序使用 Windows 多媒体混音器*Xxx* 函数来浏览拓扑，方法是枚举每个路径上的节点序列。 例如，在发现卷级控制节点后，应用程序可以设置该节点上的音量级别。 有关 Windows 多媒体的详细信息，请参阅 Microsoft Windows SDK 文档。 有关通过混音器*Xxx* 函数表示 KS 拓扑的详细信息，请参阅 [音频混音器 API 转换的内核流拓扑](kernel-streaming-topology-to-audio-mixer-api-translation.md)。

PortCls 提供六个端口驱动程序： WavePci、WaveCyclic、WaveRT、MIDI、Dmu 和拓扑。 自 Windows Vista 起， (WaveRT 已可用，并且是建议的方法。 ) 拓扑端口驱动程序控制音频适配器电路的部分，该部分将呈现流从 wave 设备和 MIDI 设备混合在一起。 它还控制从输入插孔选择捕获流。 尽管拓扑端口驱动程序的名称有点误导，但拓扑端口驱动程序并不体现所有音频适配器的拓扑，但它通常包含其中的大部分功能。 其他端口驱动程序会提供适配器拓扑的剩余部分。

每个端口驱动程序与相应的微型端口驱动程序配对，以形成代表音频适配器上 (波浪、MIDI 或混音器) 的特定设备的 [KS 筛选器](../stream/ks-filters.md) ，如下表所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">筛选器类型</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>波浪<em>Xxx</em> 筛选器</p></td>
<td align="left"><p>表示一个波形设备，该设备将波形输出流转换为模拟音频信号，或将模拟音频信号转换为波形输入流。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MIDI 或 Dmu 筛选器</p></td>
<td align="left"><p>表示播放或捕获 MIDI 流的 MIDI 设备。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>拓扑筛选器</p></td>
<td align="left"><p>表示适配器的混合器电路。</p></td>
</tr>
</tbody>
</table>

 

微型端口驱动程序实现了筛选器的设备特定函数，包括设备包含的适配器拓扑部分的定义。 端口驱动程序负责处理每种类型的筛选器的一般筛选器操作，包括与操作系统的通信。

每个筛选器都有一个或多个 [KS pin](../stream/ks-pins.md) ，用作音频数据流的路径以输入和离开筛选器。 通常，拓扑筛选器上的 pin 通过适配器电路中的硬编码连接绑定到 wave、MIDI 和 Dmu 筛选器的针脚。 这些筛选器及其相互联系形成了一个表示适配器拓扑的 KS 筛选器图。

下图显示了一个示例音频适配器的拓扑。

![说明音频适配器拓扑的示意图](images/topoexample.png)

在上图中，位于顶层的拓扑包含 MIDI、波浪*Xxx*和拓扑筛选器之间的连接。 此外，每个筛选器都具有自己的内部拓扑，其中包含通过筛选器和位于每个路径中的控制节点的数据路径。 节点标记如下表中所示。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Label</th>
<th align="left">说明</th>
<th align="left">KS 节点类型 GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>合成</p></td>
<td align="left"><p>合成器节点</p></td>
<td align="left"><a href="/windows-hardware/drivers/audio/ksnodetype-synthesizer" data-raw-source="[&lt;strong&gt;KSNODETYPE_SYNTHESIZER&lt;/strong&gt;](./ksnodetype-synthesizer.md)"><strong>KSNODETYPE_SYNTHESIZER</strong></a></td>
</tr>
<tr class="even">
<td align="left"><p>DAC</p></td>
<td align="left"><p>数字到音频转换器节点</p></td>
<td align="left"><a href="/windows-hardware/drivers/audio/ksnodetype-dac" data-raw-source="[&lt;strong&gt;KSNODETYPE_DAC&lt;/strong&gt;](./ksnodetype-dac.md)"><strong>KSNODETYPE_DAC</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p>ADC</p></td>
<td align="left"><p>模拟到数字转换器节点</p></td>
<td align="left"><a href="/windows-hardware/drivers/audio/ksnodetype-adc" data-raw-source="[&lt;strong&gt;KSNODETYPE_ADC&lt;/strong&gt;](./ksnodetype-adc.md)"><strong>KSNODETYPE_ADC</strong></a></td>
</tr>
<tr class="even">
<td align="left"><p>Volume</p></td>
<td align="left"><p>卷级控制节点</p></td>
<td align="left"><a href="/windows-hardware/drivers/audio/ksnodetype-volume" data-raw-source="[&lt;strong&gt;KSNODETYPE_VOLUME&lt;/strong&gt;](./ksnodetype-volume.md)"><strong>KSNODETYPE_VOLUME</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p>静音</p></td>
<td align="left"><p>静音控制节点</p></td>
<td align="left"><a href="/windows-hardware/drivers/audio/ksnodetype-mute" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUTE&lt;/strong&gt;](./ksnodetype-mute.md)"><strong>KSNODETYPE_MUTE</strong></a></td>
</tr>
<tr class="even">
<td align="left"><p>Sum</p></td>
<td align="left"><p>求和节点</p></td>
<td align="left"><a href="/windows-hardware/drivers/audio/ksnodetype-sum" data-raw-source="[&lt;strong&gt;KSNODETYPE_SUM&lt;/strong&gt;](./ksnodetype-sum.md)"><strong>KSNODETYPE_SUM</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p>混合</p></td>
<td align="left"><p>多路复用器节点</p></td>
<td align="left"><a href="/windows-hardware/drivers/audio/ksnodetype-mux" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUX&lt;/strong&gt;](./ksnodetype-mux.md)"><strong>KSNODETYPE_MUX</strong></a></td>
</tr>
</tbody>
</table>

在上图中，音频适配器左侧的针脚表示逻辑连接 (不是物理连接) 通过这些连接，数据流从系统总线进入适配器，或从适配器输入系统总线。 这些 pin 以逻辑方式连接到其他筛选器上的源和接收器插针 (不显示在适配器外部) 。 通常，这些筛选器是软件模块，它们与适配器拓扑一起形成更大的筛选器图，应用程序可以使用混音器*Xxx* 函数来浏览其拓扑。 例如，上图中标记为 "PCM Wave Out" 的 pin 以逻辑方式连接到 Windows 中的用户模式音频引擎。 这些逻辑连接通过系统总线上的 DMA 传输来维护。

与此相反，拓扑筛选器左边缘上的针脚以物理方式连接到 MIDI 和波浪*Xxx* 筛选器。 这些连接是硬编码的，不能被软件更改。

音频适配器右侧的桥接插针表示系统机箱上的音频插孔。 这些 pin 称为 *桥* 接，因为它们会将 KS 筛选器关系图与外部环境之间的边界桥接。

筛选器、pin 和节点通常具有属性，这些属性可供客户端 (内核模式组件或音频驱动程序的用户模式应用程序) 访问。 客户端可以向筛选器、pin 或节点发送 [KS 属性请求](../stream/ks-properties.md) ，以查询属性的当前值或更改属性值。 例如，卷级别控制节点有一个 [**KSPROPERTY \_ AUDIO \_ VOLUMELEVEL**](./ksproperty-audio-volumelevel.md) 属性，客户端可以通过 KS 属性请求更改该属性。 求和节点是通常没有属性的节点类型的示例。

为简单起见，上图中的波浪*Xxx* 筛选器仅提供了一个用于接受来自系统总线的 PCM 波形输出流的 pin。 与此相反，某些波形设备为 PCM 波纹输出提供多个 pin，并包含用于内部混合输入 pin 的流的硬件。 这些设备通过接受从应用程序的声音缓冲区播放的 PCM 流，为使用 DirectSound 的应用程序提供硬件加速。 为了使 DirectSound 使用这些 pin，它们必须为二维 (二维) 和三维 (3D) 处理提供其他节点，如 [WDM 音频中的 DirectSound 硬件加速](directsound-hardware-acceleration-in-wdm-audio.md)中所述。

此类型的硬件加速在 Windows Server 2003、Windows XP、Windows 2000 和 Windows Me/98 中受支持，但在 Windows Vista 中不受支持。 Windows Vista 不会在较旧的波形设备上使用硬件加速 pin。

在上图中，MIDI、波浪*Xxx*和拓扑之间的物理连接将筛选所有传输模拟音频信号。 但是，不同的拓扑设备可能会从 MIDI 和 wave 设备接受数字输出流，对其进行数字混合，并将数字混合转换为模拟输出信号，从而实现类似的效果。

上图左下角的 "非 PCM 向外" 图钉接受 S/PDIF 传递格式的非 PCM 输出流，如 AC-3-S/PDIF 或 WMA Pro-over S/PDIF 的输出流。 使用其中一种格式时，设备只需在不解码数据的情况下传输 S/PDIF 链接上的压缩数据。 出于此原因，上图右下角的 "S/PDIF Out" pin 的数据路径不包含卷或静音节点。 有关非 PCM 音频格式和 S/PDIF 传递传输的详细信息，请参阅支持非 pcm [波浪格式](supporting-non-pcm-wave-formats.md) 和 [非 Pcm 流的 s/pdif 传递传输](s-pdif-pass-through-transmission-of-non-pcm-streams.md)。

微型端口驱动程序以 [**PCFILTER \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor) 结构的形式向端口驱动程序呈现其拓扑。 此结构描述了筛选器的所有 pin 和节点，并指定了 pin 和节点相互连接的方式。

可以将音频适配器中的混音器电路分区为多个拓扑筛选器，而不是按上图所示设计单一拓扑结构筛选器。 例如，在上图中，驱动扬声器的数据路径可能作为一个拓扑筛选器实现，从输入设备中捕获音频数据的数据路径可作为单独的拓扑筛选器实现。 如果未使用特定拓扑筛选器中的数据路径，则可以关闭该部分适配器，而不会禁用整个适配器。 有关详细信息，请参阅 [动态音频 Subdevices](dynamic-audio-subdevices.md)。