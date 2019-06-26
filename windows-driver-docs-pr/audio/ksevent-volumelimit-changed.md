---
title: KSEVENT\_VOLUMELIMIT\_已更改
description: KSEVENT\_VOLUMELIMIT\_CHANGED 事件指示音频堆栈为音频设备的音频音量级别限制已更改。
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
ms.openlocfilehash: 96ac4f7cf4078420efd7464a519699ad0be3d000
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391519"
---
# <a name="kseventvolumelimitchanged"></a>KSEVENT\_VOLUMELIMIT\_已更改


KSEVENT\_VOLUMELIMIT\_CHANGED 事件指示音频堆栈为音频设备的音频音量级别限制已更改。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespan-usage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span> 使用率摘要表

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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

事件值类型 （操作数据） 是**KSEVENTDATA**结构，它指定要使用此事件的通知方法。

<a name="remarks"></a>备注
-------

有关如何实现对 KSEVENT 的支持信息\_PINCAPS\_VOLUMELIMITCHANGE 事件，请参阅**备注**一部分[ **KSEVENT\_PINCAPS\_格式**](ksevent-pincaps-formatchange.md)。

请注意，尽管 KSEVENT\_PINCAPS\_格式批筛选器 （用于微型端口驱动程序链接到 Portcls），通过实现 KSEVENT\_VOLUMELIMIT\_在拓扑上实现已更改事件筛选器。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSEVENT\_PINCAPS\_格式**](ksevent-pincaps-formatchange.md)

[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)

 

 






