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
ms.openlocfilehash: 8cd7d840280121ffac3ea634f95be85ad247d02f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564335"
---
# <a name="video-compression-properties"></a>视频压缩属性


[PROPSETID\_VIDCAP\_VIDEOCOMPRESSION](https://msdn.microsoft.com/library/windows/hardware/ff567813)属性集包含与视频压缩相关的属性。 下表介绍的属性属于 PROPSETID\_VIDCAP\_VIDEOCOMPRESSION 属性集。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565975" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_GETINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565975)"><strong>KSPROPERTY_VIDEOCOMPRESSION_GETINFO</strong></a></p></td>
<td><p>返回有关视频压缩功能的设备的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565986" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_KEYFRAME_RATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565986)"><strong>KSPROPERTY_VIDEOCOMPRESSION_KEYFRAME_RATE</strong></a></p></td>
<td><p>控制视频的压缩的关键帧速率。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565991" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_FRAME_SIZE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565991)"><strong>KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_FRAME_SIZE</strong></a></p></td>
<td><p>指定临时的新的帧大小以覆盖当前的大小。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566004" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_KEYFRAME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566004)"><strong>KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_KEYFRAME</strong></a></p></td>
<td><p>指定临时的新的关键帧速率重写的当前速率。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566009" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566009)"><strong>KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME</strong></a></p></td>
<td><p>控制预测的帧间隔。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566015" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_QUALITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566015)"><strong>KSPROPERTY_VIDEOCOMPRESSION_QUALITY</strong></a></p></td>
<td><p>控制设置的视频的压缩质量。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566019" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566019)"><strong>KSPROPERTY_VIDEOCOMPRESSION_WINDOWSIZE</strong></a></p></td>
<td><p>控制平均视频帧的数据的速率。</p></td>
</tr>
</tbody>
</table>

 

 

 




