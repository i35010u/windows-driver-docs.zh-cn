---
title: 视频解码器属性
description: 视频解码器属性
ms.assetid: 671a310b-52a6-49f0-8848-e586a37c25ff
keywords:
- 视频解码器属性 WDK 视频捕获
- 解码器属性 WDK 视频捕获
- PROPSETID_VIDCAP_VIDEODECODER
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62a471ae2898091949e46f8652bc2adeb208e066
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359619"
---
# <a name="video-decoder-properties"></a>视频解码器属性


[PROPSETID\_VIDCAP\_VIDEODECODER](https://msdn.microsoft.com/library/windows/hardware/ff568121)属性集包含与模拟视频解码器的设备，该操作相关的属性，例如传输标准和计时发出信号。 下表介绍的属性属于 PROPSETID\_VIDCAP\_VIDEODECODER 属性集。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_VIDEODECODER KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566046" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566046)"><strong>KSPROPERTY_VIDEODECODER_CAPS</strong></a></p></td>
<td><p>返回的视频解码器设备，如信号标准 (NTSC、 PAL、 SECAM) 和处置时间的功能的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566058" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STANDARD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566058)"><strong>KSPROPERTY_VIDEODECODER_STANDARD</strong></a></p></td>
<td><p>控制的当前模拟视频标准。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566060" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566060)"><strong>KSPROPERTY_VIDEODECODER_STATUS</strong></a></p></td>
<td><p>返回视频解码设备，如视频信号中的行数和是否已锁定该信号的状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566051" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566051)"><strong>KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE</strong></a></p></td>
<td><p>控制三状态输出的视频解码器。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566062" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_VCR_TIMING&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566062)"><strong>KSPROPERTY_VIDEODECODER_VCR_TIMING</strong></a></p></td>
<td><p>控制视频解码器使用 VCR 计时或广播的计时。</p></td>
</tr>
</tbody>
</table>

 

 

 




