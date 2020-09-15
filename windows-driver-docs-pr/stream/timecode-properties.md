---
title: 时间码属性
description: 时间码属性
ms.assetid: e8359778-8cc6-4f19-b869-f9597dae0502
keywords:
- 时间码属性 WDK 视频捕获
- PROPSETID_TIMECODE_READER
- 磁带时间码属性 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28225842151a6f616fbd25deeea79cd1ff75c29b
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104898"
---
# <a name="timecode-properties"></a>时间码属性


[PROPSETID 时间 \_ 码 \_ 读取器](./propsetid-timecode-reader.md)属性集包含与磁带上时间码相关的属性，例如 DVHS 磁带卡座或 MiniDV 摄像机。 下表描述了属于 PROPSETID 时间 \_ 码 \_ 读取器属性集的属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_TIMECODE_READER KS 属性</th>
<th>属性说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-timecode-reader" data-raw-source="[&lt;strong&gt;KSPROPERTY_TIMECODE_READER&lt;/strong&gt;](./ksproperty-timecode-reader.md)"><strong>KSPROPERTY_TIMECODE_READER</strong></a></p></td>
<td><p>返回当前磁带位置的时间码。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-atn-reader" data-raw-source="[&lt;strong&gt;KSPROPERTY_ATN_READER&lt;/strong&gt;](./ksproperty-atn-reader.md)"><strong>KSPROPERTY_ATN_READER</strong></a></p></td>
<td><p>返回当前磁带位置的绝对磁道号。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksproperty-rtc-reader" data-raw-source="[&lt;strong&gt;KSPROPERTY_RTC_READER&lt;/strong&gt;](./ksproperty-rtc-reader.md)"><strong>KSPROPERTY_RTC_READER</strong></a></p></td>
<td><p>返回当前磁带位置的相对时间计数器。</p></td>
</tr>
</tbody>
</table>

 

