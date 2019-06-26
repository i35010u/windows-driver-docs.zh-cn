---
title: 电视音频属性
description: 电视音频属性
ms.assetid: 0eed4007-9fd9-4927-8ac7-2e23fd082dec
keywords:
- 电视音频属性 WDK 视频捕获
- 音频属性 WDK 视频捕获
- PROPSETID_VIDCAP_TVAUDIO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b094344eb42f3d63bdc06d407fee9041c73f629
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377719"
---
# <a name="tv-audio-properties"></a>电视音频属性


[PROPSETID\_VIDCAP\_TVAUDIO](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-tvaudio)属性集包含与电视音频相关的属性。 下表介绍的属性属于 PROPSETID\_VIDCAP\_TVAUDIO 属性集。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_TVAUDIO KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tvaudio-caps" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_CAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tvaudio-caps)"><strong>KSPROPERTY_TVAUDIO_CAPS</strong></a></p></td>
<td><p>返回电视音频设备，如硬件是否支持 mono 或立体声音频和 SAP 的功能信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tvaudio-currently-available-modes" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tvaudio-currently-available-modes)"><strong>KSPROPERTY_TVAUDIO_CURRENTLY_AVAILABLE_MODES</strong></a></p></td>
<td><p>返回当前可用的电视音频模式，在该属性进行了查询的时间。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tvaudio-mode" data-raw-source="[&lt;strong&gt;KSPROPERTY_TVAUDIO_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tvaudio-mode)"><strong>KSPROPERTY_TVAUDIO_MODE</strong></a></p></td>
<td><p>控制电视音频设备的当前音频模式。</p></td>
</tr>
</tbody>
</table>

 

 

 




