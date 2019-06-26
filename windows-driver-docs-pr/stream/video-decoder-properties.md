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
ms.openlocfilehash: 488c8668d3287f452a7aa789cc0450fb101a58be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385370"
---
# <a name="video-decoder-properties"></a>视频解码器属性


[PROPSETID\_VIDCAP\_VIDEODECODER](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videodecoder)属性集包含与模拟视频解码器的设备，该操作相关的属性，例如传输标准和计时发出信号。 下表介绍的属性属于 PROPSETID\_VIDCAP\_VIDEODECODER 属性集。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-caps)"><strong>KSPROPERTY_VIDEODECODER_CAPS</strong></a></p></td>
<td><p>返回的视频解码器设备，如信号标准 (NTSC、 PAL、 SECAM) 和处置时间的功能的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-standard" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STANDARD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-standard)"><strong>KSPROPERTY_VIDEODECODER_STANDARD</strong></a></p></td>
<td><p>控制的当前模拟视频标准。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-status" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_STATUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-status)"><strong>KSPROPERTY_VIDEODECODER_STATUS</strong></a></p></td>
<td><p>返回视频解码设备，如视频信号中的行数和是否已锁定该信号的状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-output-enable" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-output-enable)"><strong>KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE</strong></a></p></td>
<td><p>控制三状态输出的视频解码器。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-vcr-timing" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_VCR_TIMING&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videodecoder-vcr-timing)"><strong>KSPROPERTY_VIDEODECODER_VCR_TIMING</strong></a></p></td>
<td><p>控制视频解码器使用 VCR 计时或广播的计时。</p></td>
</tr>
</tbody>
</table>

 

 

 




