---
title: 拓扑节点
description: 拓扑节点
ms.assetid: 39827413-2b6b-4925-97bb-e0f3e3428b13
keywords:
- 拓扑节点 WDK 音频
- 节点 WDK 音频，拓扑
- MIXERCONTROL 结构
- 声调节点 WDK 音频
- 翻译节点 WDK 音频
- supermix 节点 WDK 音频
- 低音属性 WDK 音频
- 高音属性 WDK 音频
- 低音增强属性 WDK 音频
- 中间频率属性 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ffd75cd453016ebc9ad75ba8334f5b6801d09b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829998"
---
# <a name="topology-nodes"></a>拓扑节点


## <span id="topology_nodes"></span><span id="TOPOLOGY_NODES"></span>


音频应用程序可以通过 Microsoft Windows 多媒体函数[**mixerGetLineControls**](https://docs.microsoft.com/previous-versions/dd757302(v=vs.85))访问混音器控件。 此函数检索一个或多个 MIXERCONTROL 结构的数组，其中每个结构都描述音频线上单个控件节点的状态和指标。 MIXERCONTROL 结构的**dwControlType**成员设置为指定控件类型的枚举值。 已为音频 Vxd 指定了多个混合器控件类型，但只有这些控件的一个子集可用于 WDM 音频驱动程序。

WDMAud 将部分（而不是所有）拓扑节点转换为相应的混音器控件。 下表中列出的拓扑节点类型具有与混合器控件相同的对应项。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">节点类型</th>
<th align="left">拓扑-节点类型名称</th>
<th align="left">混合器控件类型名称</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AGC</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-agc" data-raw-source="[&lt;strong&gt;KSNODETYPE_AGC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-agc)"><strong>KSNODETYPE_AGC</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_ONOFF</p></td>
</tr>
<tr class="even">
<td align="left"><p>响度</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-loudness" data-raw-source="[&lt;strong&gt;KSNODETYPE_LOUDNESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-loudness)"><strong>KSNODETYPE_LOUDNESS</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_LOUDNESS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Mute</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mute" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUTE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mute)"><strong>KSNODETYPE_MUTE</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_MUTE</p></td>
</tr>
<tr class="even">
<td align="left"><p>音调（多个）</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-tone" data-raw-source="[&lt;strong&gt;KSNODETYPE_TONE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-tone)"><strong>KSNODETYPE_TONE</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_ONOFF （如果支持 KSPROPERTY_AUDIO_BASS_BOOST）</p>
<p>MIXERCONTROL_CONTROLTYPE_BASS （如果支持 KSPROPERTY_AUDIO_BASS）</p>
<p>MIXERCONTROL_CONTROLTYPE_TREBLE （如果支持 KSPROPERTY_AUDIO_TREBLE）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Volume</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume" data-raw-source="[&lt;strong&gt;KSNODETYPE_VOLUME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)"><strong>KSNODETYPE_VOLUME</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_VOLUME</p></td>
</tr>
<tr class="even">
<td align="left"><p>Peakmeter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-peakmeter" data-raw-source="[&lt;strong&gt;KSNODETYPE_PEAKMETER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-peakmeter)"><strong>KSNODETYPE_PEAKMETER</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_PEAKMETER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>混合</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux)"><strong>KSNODETYPE_MUX</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_MUX</p></td>
</tr>
<tr class="even">
<td align="left"><p>立体声宽</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-stereo-wide" data-raw-source="[&lt;strong&gt;KSNODETYPE_STEREO_WIDE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-stereo-wide)"><strong>KSNODETYPE_STEREO_WIDE</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_FADER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Chorus</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-chorus" data-raw-source="[&lt;strong&gt;KSNODETYPE_CHORUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-chorus)"><strong>KSNODETYPE_CHORUS</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_FADER</p></td>
</tr>
<tr class="even">
<td align="left"><p>混响</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-reverb" data-raw-source="[&lt;strong&gt;KSNODETYPE_REVERB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-reverb)"><strong>KSNODETYPE_REVERB</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_FADER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Supermix （多个）</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-supermix" data-raw-source="[&lt;strong&gt;KSNODETYPE_SUPERMIX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-supermix)"><strong>KSNODETYPE_SUPERMIX</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_MUTE （如果 supermix 节点支持 KSPROPERTY_AUDIO_MUTE）</p>
<p>MIXERCONTROL_CONTROLTYPE_VOLUME （请参阅文本中的注释）</p></td>
</tr>
</tbody>
</table>

 

"拓扑"-上表中缺少的节点类型不会转换为混音器控件，并且 WDM 音频驱动程序不支持表中缺少的混合器控件。

请注意，表中缺少 MIXERCONTROL\_CONTROLTYPE\_自定义。 这意味着 WDM 音频驱动程序不支持自定义混音器控件。

[**声调节点**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-tone)支持四个属性：[**低音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass)、[**高音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-treble)、[**中频率**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mid)和[**低音增强**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass-boost)。 中间频率属性没有与混音器对应的行，但还有其他三个属性。 对于拓扑中发现的每个色调节点，会对每个支持的属性进行查询：

[**KSPROPERTY\_音频\_低音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass)

[**KSPROPERTY\_音频\_高音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-treble)

[**KSPROPERTY\_音频\_低音\_提高**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass-boost)

成功的每个属性查询将生成一个混音器控件。 由于命名问题，单色调节点应仅支持一个属性。 例如，如果设备支持低音和高音，则它应具有两个声调节点，以便节点可以具有不同的名称。

[**Supermix 节点**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-supermix)最多支持两个控件：静音和音量。 当 supermix 节点满足 supermix 节点的 "[**功能" 表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table)中的每个条目的至少两个条件之一时，可以将该节点用作静音控件：

-   该条目支持 "静音" 属性，由**功能**指定。**静音**标志。

-   条目为完全衰减（-无限大分贝衰减），并且无法打开，这是由这两个**功能**指定的。**最小**和**功能**。值**长\_** MIN （0x80000000）。

当 supermix 功能表中的每个项都有一个非零范围时，supermix 节点可以用作卷控件。 所有其他控件都转换为一对一。 当遇到识别的节点时，混音器驱动程序将查询该节点的相应属性。

若要检查立体声或 mono 支持，请先查询左通道，然后再执行右通道，最后，如果这两种方法都失败，则将尝试使用主通道（-1）。 如果这些查询都不成功，则不会为该节点生成控件。 请注意，不会查询每个通道的 MUX 节点。 相反，将执行单个查询来检索当前的 MUX 选择。

查询节点的名称时，该控件的名称将以字符串形式返回[ **\_拓扑\_name**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-name)属性。 如果某个节点生成了多个控件，则所有控件共享同一名称。

 

 




