---
title: KSEVENT\_VOLUMELIMIT\_更改
description: KSEVENT\_VOLUMELIMIT\_CHANGED 事件向音频堆栈表明音频设备的音频音量级别限制已更改。
ms.assetid: CC6A6027-03CA-4D2C-8AA2-155E1617E19B
keywords:
- KSEVENT_VOLUMELIMIT_CHANGED 音频设备
topic_type:
- apiref
api_name:
- KSEVENT_VOLUMELIMIT_CHANGED
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 548f95309cfa8180983b36a137e6786f4a17db7d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833104"
---
# <a name="ksevent_volumelimit_changed"></a>KSEVENT\_VOLUMELIMIT\_更改


KSEVENT\_VOLUMELIMIT\_CHANGED 事件向音频堆栈表明音频设备的音频音量级别限制已更改。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespan-usage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

事件值类型（操作数据）是指定要用于此事件的通知方法的**KSEVENTDATA**结构。

<a name="remarks"></a>备注
-------

有关如何为 KSEVENT\_PINCAPS\_VOLUMELIMITCHANGE 事件实现支持的信息，请参阅[**KSEVENT\_PINCAPS\_FORMATCHANGE**](ksevent-pincaps-formatchange.md)的 "**备注**" 部分。

请注意，虽然在 Wave 筛选器上实现了 KSEVENT\_PINCAPS\_FORMATCHANGE （对于链接到 Portcls 的微型端口驱动程序），KSEVENT\_VOLUMELIMIT\_CHANGED 事件是在拓扑筛选器上实现的。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSEVENT\_PINCAPS\_FORMATCHANGE**](ksevent-pincaps-formatchange.md)

[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

 

 






