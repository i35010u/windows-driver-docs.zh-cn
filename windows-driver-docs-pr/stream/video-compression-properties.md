---
title: 视频压缩属性
description: 视频压缩属性
ms.assetid: 2fd69425-7c36-4766-88e6-7f02d5fa6659
keywords:
- 视频的压缩属性 WDK 视频捕获
- 压缩属性 WDK 视频捕获
- PROPSETID_VIDCAP_VIDEOCOMPRESSION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0330f42fe280af707fb98d02db65d60d10b9d7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385379"
---
# <a name="video-compression-properties"></a>视频压缩属性


[PROPSETID\_VIDCAP\_VIDEOCOMPRESSION](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videocompression)属性集包含与视频压缩相关的属性。 下表介绍的属性属于 PROPSETID\_VIDCAP\_VIDEOCOMPRESSION 属性集。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_VIDEOCOMPRESSION KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-getinfo" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_GETINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-getinfo)"><strong>KSPROPERTY_VIDEOCOMPRESSION_GETINFO</strong></a></p></td>
<td><p>返回有关视频压缩功能的设备的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-keyframe-rate" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_KEYFRAME_RATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-keyframe-rate)"><strong>KSPROPERTY_VIDEOCOMPRESSION_KEYFRAME_RATE</strong></a></p></td>
<td><p>控制视频的压缩的关键帧速率。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-override-frame-size" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_FRAME_SIZE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-override-frame-size)"><strong>KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_FRAME_SIZE</strong></a></p></td>
<td><p>指定临时的新的帧大小以覆盖当前的大小。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-override-keyframe" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_KEYFRAME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-override-keyframe)"><strong>KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_KEYFRAME</strong></a></p></td>
<td><p>指定临时的新的关键帧速率重写的当前速率。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-pframes-per-keyframe" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-pframes-per-keyframe)"><strong>KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME</strong></a></p></td>
<td><p>控制预测的帧间隔。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-quality" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_QUALITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-quality)"><strong>KSPROPERTY_VIDEOCOMPRESSION_QUALITY</strong></a></p></td>
<td><p>控制设置的视频的压缩质量。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-windowsize" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-videocompression-windowsize)"><strong>KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE</strong></a></p></td>
<td><p>控制平均视频帧的数据的速率。</p></td>
</tr>
</tbody>
</table>

 

 

 




