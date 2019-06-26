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
ms.openlocfilehash: f8c5420e648bfd3217caecdfee07e5d877341cd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377735"
---
# <a name="timecode-properties"></a>时间码属性


[PROPSETID\_时间码\_读取器](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-timecode-reader)属性集包含磁带，例如 DVHS 磁带一副纸牌或 MiniDV 摄像机上的时间码与相关的属性。 下表介绍的属性属于 PROPSETID\_时间码\_读取器属性集。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-timecode-reader" data-raw-source="[&lt;strong&gt;KSPROPERTY_TIMECODE_READER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-timecode-reader)"><strong>KSPROPERTY_TIMECODE_READER</strong></a></p></td>
<td><p>返回当前磁带位置的时间代码。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-atn-reader" data-raw-source="[&lt;strong&gt;KSPROPERTY_ATN_READER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-atn-reader)"><strong>KSPROPERTY_ATN_READER</strong></a></p></td>
<td><p>返回当前磁带位置的绝对跟踪号。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-rtc-reader" data-raw-source="[&lt;strong&gt;KSPROPERTY_RTC_READER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-rtc-reader)"><strong>KSPROPERTY_RTC_READER</strong></a></p></td>
<td><p>返回当前磁带位置的相对时间计数器。</p></td>
</tr>
</tbody>
</table>

 

 

 




