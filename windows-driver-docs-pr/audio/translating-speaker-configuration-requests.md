---
title: 转换 Speaker-Configuration 请求
description: 转换 Speaker-Configuration 请求
ms.assetid: be3dce30-7395-4332-ba62-de9a718b62f5
keywords:
- 转换扬声器配置请求 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c2b7d76dbe64d6e9ef547fe5ad3c828575d806e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335416"
---
# <a name="translating-speaker-configuration-requests"></a>转换 Speaker-Configuration 请求


## <span id="translating_speaker_configuration_requests"></span><span id="TRANSLATING_SPEAKER_CONFIGURATION_REQUESTS"></span>


**请注意**  此信息适用于 Windows XP 和早期版本的操作系统。 从 Windows Vista 开始**IDirectSound::GetSpeakerConfig**并**IDirectSound::SetSpeakerConfig**已弃用。

 

当应用程序调用**IDirectSound::SetSpeakerConfig** （请参阅 Microsoft Windows SDK 文档） 若要更改扬声器配置，DirectSound 转换指定的 DSSPEAKER\_*Xxx*扬声器配置参数等效 KSAUDIO\_*Xxx*通道配置掩码。 它将发送[ **KSPROPERTY\_音频\_通道\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff537250)包含此掩码表示 DirectSound 设备筛选的组属性请求。

在下面的表中，每个 DSSPEAKER\_*Xxx*左侧的参数与等效 KSAUDIO 配对\_*Xxx*在右侧的通道配置掩码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DSSPEAKER 参数</th>
<th align="left">KSAUDIO 通道配置掩码</th>
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

 

在上表中，DirectSound 其耳机和立体声扬声器配置指定具有相同通道掩码 KSAUDIO\_演讲者\_立体声。 若要区分这两个配置，DirectSound 发送筛选器指定演讲者几何图形的第二个集属性请求 (请参阅[ **KSPROPERTY\_音频\_立体声\_说话人\_几何图形**](https://msdn.microsoft.com/library/windows/hardware/ff537305))。 若要指示耳机，DirectSound 将值传递 KSAUDIO\_立体声\_演讲者\_GEOMETRY\_耳机使用说话人 geometry 请求。

对于立体扬声器，但是，调用方流入**SetSpeakerConfig**可以指定一个或多个可能 DSSPEAKER\_*Xxx*立体声演讲者几何图形。 这些包中的以下表和等效 KSAUDIO 左列显示\_*Xxx*参数显示在右侧。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DSSPEAKER 立体声演讲者 Geometry</th>
<th align="left">KSAUDIO 立体声演讲者 Geometry</th>
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

 

如果调用方没有显式指定一个几何图形的上面的左侧列中，DirectSound 假定 DSSPEAKER\_几何图形\_宽默认情况下。

 

 




