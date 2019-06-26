---
title: 拓扑节点
description: 拓扑节点
ms.assetid: 39827413-2b6b-4925-97bb-e0f3e3428b13
keywords:
- 拓扑节点 WDK 音频
- 节点 WDK 音频，拓扑
- MIXERCONTROL 结构
- 音节点 WDK 音频
- 转换节点 WDK 音频
- supermix 节点 WDK 音频
- 低音属性 WDK 音频
- 高音属性 WDK 音频
- 低音增强属性 WDK 音频
- 中间 frequency 属性 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9dfe893aaa5e301ab9de219c337f6ab34456ad6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354175"
---
# <a name="topology-nodes"></a>拓扑节点


## <span id="topology_nodes"></span><span id="TOPOLOGY_NODES"></span>


音频应用程序可以通过 Microsoft Windows 多媒体函数访问混音器控件[ **mixerGetLineControls**](https://docs.microsoft.com/previous-versions/dd757302(v=vs.85))。 此函数可检索一个或多个 MIXERCONTROL 结构数组，其中每个音频行描述的状态和度量值的单个控件节点。 **DwControlType** MIXERCONTROL 结构中的成员设置为一个枚举值，指定的控件类型。 Mixer 控件类型的数量已指定用于音频 Vxd，但这些控件的一个子集是适用于 WDM 音频驱动程序。

WDMAud 转换对应的混音器行控件为某些但并非所有拓扑节点。 下表中列出的拓扑节点类型具有混音器行的控件的对应项。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">节点类型</th>
<th align="left">拓扑节点类型名称</th>
<th align="left">Mixer 控件类型名称</th>
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
<td align="left"><p>音 （多个）</p></td>
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
<td align="left"><p>MUX</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux)"><strong>KSNODETYPE_MUX</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_MUX</p></td>
</tr>
<tr class="even">
<td align="left"><p>立体声宽</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-stereo-wide" data-raw-source="[&lt;strong&gt;KSNODETYPE_STEREO_WIDE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-stereo-wide)"><strong>KSNODETYPE_STEREO_WIDE</strong></a></p></td>
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_FADER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>合唱团</p></td>
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
<td align="left"><p>MIXERCONTROL_CONTROLTYPE_MUTE （如果 KSPROPERTY_AUDIO_MUTE supermix 节点中受支持）</p>
<p>MIXERCONTROL_CONTROLTYPE_VOLUME （请参阅中的文本的注释）</p></td>
</tr>
</tbody>
</table>

 

上表中缺少的拓扑节点类型不转换为 mixer 行控件，并通过 WDM 音频驱动程序不支持在表中缺少的混音器行控件。

请注意该 MIXERCONTROL\_CONTROLTYPE\_自定义缺少表。 这意味着，WDM 音频驱动程序不支持自定义混音器控件。

一个[**音节点**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-tone)支持四个属性： [**低音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass)， [**高音**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-treble)， [**中间频率**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mid)，并且[**低音增强**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass-boost)。 中间频率属性没有 mixer 行对应，但其他三个属性执行操作。 对于在拓扑中发现每个音节点，为每个受支持的属性进行查询：

[**KSPROPERTY\_AUDIO\_BASS**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass)

[**KSPROPERTY\_AUDIO\_TREBLE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-treble)

[**KSPROPERTY\_AUDIO\_BASS\_BOOST**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-bass-boost)

每个成功的属性查询生成的混音器行控件。 由于命名问题，而单个音节点应支持只有一个属性。 如果设备支持高音和低音，例如，它应具有两个音节点，以便在节点可以具有不同的名称。

一个[ **supermix 节点**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-supermix)支持最多两个控件： 静音和卷。 Supermix 节点可用作静音控件，当它满足至少一个这两个条件 supermix 节点中的每个条目时[**功能表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixcap_table):

-   该条目支持静音属性，由指定**功能**。**静音**标志。

-   该条目完全衰减 (-无穷大分贝衰减) 和不能调高，其指定由已**功能**。**最小**并**功能**。**最大**值为长时间\_最小值 (0x80000000)。

Supermix 节点可以用作 supermix 功能表中的每个条目具有非零值的范围内时的音量控件。 所有其他控件将转换一对一。 当遇到已识别的节点时，mixer 行驱动程序将查询该节点的相应属性。

若要检查立体声或 mono 支持，左的通道进行查询后, 跟右通道中，并最后，如果这两种失败，则尝试主通道 (-1)。 如果没有任何这些查询成功，没有控件生成该节点。 请注意 MUX 节点不为每个通道进行查询。 而被执行单个查询来检索当前 MUX 所选内容。

查询节点时，作为字符串返回控件的名称及其[ **KSPROPERTY\_拓扑\_名称**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-name)属性。 如果某个节点生成多个控件，所有控件都共享相同的名称。

 

 




