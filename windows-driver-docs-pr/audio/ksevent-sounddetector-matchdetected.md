---
title: KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED
description: KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED 事件生成的音频驱动程序以通知操作系统，每当检测到匹配项。
ms.assetid: 595EBC90-3903-495C-9811-A47B7BC4D98D
keywords:
- KSEVENT_SOUNDDETECTOR_MATCHDETECTED 音频设备
topic_type:
- apiref
api_name:
- KSEVENT_SOUNDDETECTOR_MATCHDETECTED
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b37ddf2754deaabc87d516aa53e7928b2acd0af1
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391520"
---
# <a name="kseventsounddetectormatchdetected"></a>KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED


**KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED**音频驱动程序以通知操作系统，每当检测到匹配项时生成事件。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目标</th>
<th align="left">事件描述符类型</th>
<th align="left">事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

触发此事件时，OS 会读取[ **KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT** ](ksproperty-sounddetector-matchresult.md)属性。 已检测到匹配项后，音频驱动程序必须清除声音检测程序。 操作系统准备好再次等待后重装设备。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)

[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

 

 






