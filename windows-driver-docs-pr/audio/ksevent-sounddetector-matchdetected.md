---
title: KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED
description: KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED 事件由音频驱动程序生成，每当检测到匹配项时，它都会通知操作系统。
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
ms.openlocfilehash: 9952f5a13e55eb9049c8e1254ad389b46446bf0f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833105"
---
# <a name="ksevent_sounddetector_matchdetected"></a>KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED


**KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED**事件由音频驱动程序生成，每当检测到匹配项时，它都会通知操作系统。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

触发此事件时，OS 会读取[**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)属性。 检测到匹配项后，音频驱动程序必须 disarm 声音检测程序。 操作系统一旦准备好等待，rearms 设备。

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
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

 

 






