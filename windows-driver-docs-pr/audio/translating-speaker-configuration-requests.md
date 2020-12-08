---
title: 转换 Speaker-Configuration 请求
description: 转换 Speaker-Configuration 请求
keywords:
- 转换发言人-配置请求 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24e7a9237ca262a4f7131eb0ee19805eb0fc3942
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798855"
---
# <a name="translating-speaker-configuration-requests"></a>转换 Speaker-Configuration 请求


## <span id="translating_speaker_configuration_requests"></span><span id="TRANSLATING_SPEAKER_CONFIGURATION_REQUESTS"></span>


**注意**  此信息适用于 Windows XP 及更早版本的操作系统。 从 Windows Vista 开始， **IDirectSound：： GetSpeakerConfig** 和 **IDirectSound：： SetSpeakerConfig** 已弃用。

 

当应用程序调用 **IDirectSound：： SetSpeakerConfig** (参阅 Microsoft Windows SDK 文档) 若要更改扬声器配置，DirectSound 将指定的 DSSPEAKER \_ *xxx* 扬声器配置参数转换为等效的 KSAUDIO \_ *xxx* 通道配置掩码。 它将包含此掩码的 [**KSPROPERTY \_ 音频 \_ 通道 \_ 配置**](./ksproperty-audio-channel-config.md) 集-属性请求发送到表示 DirectSound 设备的筛选器。

在下表中，左侧的每个 DSSPEAKER \_ *Xxx* 参数与右侧的等效 KSAUDIO \_ *xxx* 通道配置掩码配对。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DSSPEAKER 参数</th>
<th align="left">KSAUDIO Channel-Configuration 掩码</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DSSPEAKER_DIRECTOUT</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_DIRECTOUT</p></td>
</tr>
<tr class="even">
<td align="left"><p>DSSPEAKER_HEADPHONE</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_STEREO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DSSPEAKER_MONO</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_MONO</p></td>
</tr>
<tr class="even">
<td align="left"><p>DSSPEAKER_STEREO</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_STEREO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DSSPEAKER_QUAD</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_QUAD</p></td>
</tr>
<tr class="even">
<td align="left"><p>DSSPEAKER_SURROUND</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_SURROUND</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DSSPEAKER_5POINT1</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_5POINT1</p></td>
</tr>
<tr class="even">
<td align="left"><p>DSSPEAKER_7POINT1</p></td>
<td align="left"><p>KSAUDIO_SPEAKER_7POINT1</p></td>
</tr>
</tbody>
</table>

 

在上表中，DirectSound 指定其耳机和立体声扬声器配置具有相同的通道掩码 KSAUDIO \_ 扬声器 \_ 立体声。 为了区分这两种配置，DirectSound 将筛选器发送第二个属性请求，后者指定扬声器几何 (参阅 [**KSPROPERTY \_ 音频 \_ 立体声 \_ 扬声器 \_ 几何**](./ksproperty-audio-stereo-speaker-geometry.md)) 。 为了指示耳机，DirectSound 将 KSAUDIO \_ 立体声 \_ 扬声器 \_ 几何耳机的值 \_ 与扬声器几何请求一起传递。

但对于立体声扬声器， **SetSpeakerConfig** 的调用方可以指定多个可能的 DSSPEAKER \_ *Xxx* 扬声器几何之一。 它们显示在下表的左侧列中，等效的 KSAUDIO \_ *Xxx* 参数显示在右侧。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DSSPEAKER Stereo-Speaker 几何</th>
<th align="left">KSAUDIO Stereo-Speaker 几何</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DSSPEAKER_GEOMETRY_WIDE</p></td>
<td align="left"><p>KSAUDIO_STEREO_SPEAKER_GEOMETRY_WIDE</p></td>
</tr>
<tr class="even">
<td align="left"><p>DSSPEAKER_GEOMETRY_NARROW</p></td>
<td align="left"><p>KSAUDIO_STEREO_SPEAKER_GEOMETRY_NARROW</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DSSPEAKER_GEOMETRY_MIN</p></td>
<td align="left"><p>KSAUDIO_STEREO_SPEAKER_GEOMETRY_MIN</p></td>
</tr>
<tr class="even">
<td align="left"><p>DSSPEAKER_GEOMETRY_MAX</p></td>
<td align="left"><p>KSAUDIO_STEREO_SPEAKER_GEOMETRY_MAX</p></td>
</tr>
</tbody>
</table>

 

如果调用方未显式指定上面左列中的一个几何图形，则默认情况下，DirectSound 会假定 DSSPEAKER \_ 几何图形 \_ 宽度。

 

