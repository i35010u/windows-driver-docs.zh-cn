---
title: KSNODETYPE\_PEAKMETER
description: KSNODETYPE\_PEAKMETER
ms.assetid: 11c886eb-dd63-44dd-9bca-dd19a8dd6948
keywords:
- KSNODETYPE_PEAKMETER 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_PEAKMETER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a49e0580d4525ec9aef7d98f9da4cbac45ab470
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359024"
---
# <a name="ksnodetypepeakmeter"></a>KSNODETYPE\_PEAKMETER


## <span id="ddk_ksnodetype_peakmeter_ks"></span><span id="DDK_KSNODETYPE_PEAKMETER_KS"></span>


KSNODETYPE\_PEAKMETER 节点表示硬件 peakmeter。 KS peakmeter 节点具有一个输入插针和输出插针，和两个 pin 共享相同的数据格式。

KS peakmeter 内部记录自上次复位 peakmeter 已重置为零的音频信号的最大值。 Peakmeter 自动重置本身为零后 IOCTL\_KS\_属性获取请求[ **KSPROPERTY\_音频\_PEAKMETER** ](ksproperty-audio-peakmeter.md)属性。

Peakmeter 需要硬件支持。 软件 peakmeter 不可行的并且这是因为适配器驱动程序不能访问到行中、 麦克风或其他混合和播放通道的输入存在的信号。

Microsoft 建议使 peakmeter 节点通过该流将传递筛选器内的最后一个节点。 对呈现的流，音频适配器的连接速度通常 peakmeter 节点主输出后[ **KSNODETYPE\_静音**](ksnodetype-mute.md)节点或[ **KSNODETYPE\_卷**](ksnodetype-volume.md)节点。 相同的方法适用于捕获流或任何其他流，为其筛选器包含 peakmeter 节点。

音频适配器应命名 peakmeter 节点 KSAUDFNAME\_PEAKMETER。

Peakmeter 节点应为属性标志提供属性处理程序 (请参阅[ **KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))) 下表中显示的。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">标志名称</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSPROPERTY_TYPE_GET</p></td>
<td align="left"><p>返回硬件 peakmeter 的当前值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPROPERTY_TYPE_BASICSUPPORT</p></td>
<td align="left"><p>返回一个数据区域的-32768 到 32767 之间，这是 16 位数字音频数据范围。</p></td>
</tr>
</tbody>
</table>

 

属性处理程序应验证输入的参数和左边缘和右通道信息。

Peakmeter 节点还应支持下表中的属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性名</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ksproperty-audio-peakmeter.md" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDIO_PEAKMETER&lt;/strong&gt;](ksproperty-audio-peakmeter.md)"><strong>KSPROPERTY_AUDIO_PEAKMETER</strong></a></p></td>
<td align="left"><p>表示 peakmeter 控件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ksproperty-audio-cpu-resources.md" data-raw-source="[&lt;strong&gt;KSPROPERTY_AUDIO_CPU_RESOURCES&lt;/strong&gt;](ksproperty-audio-cpu-resources.md)"><strong>KSPROPERTY_AUDIO_CPU_RESOURCES</strong></a></p></td>
<td align="left"><p>指示是否指定的节点的功能，可以使用的主机 cpu 量。</p></td>
</tr>
</tbody>
</table>

 

 

 





