---
title: KSEVENT \_ VOLUMELIMIT \_ 已更改
description: KSEVENT \_ VOLUMELIMIT \_ changed 事件向音频堆栈表明音频设备的音频音量级别限制已更改。
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
ms.openlocfilehash: 1b16a8d5b6f9a391f7acb3594b0509602858385f
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102648"
---
# <a name="ksevent_volumelimit_changed"></a>KSEVENT \_ VOLUMELIMIT \_ 已更改


KSEVENT \_ VOLUMELIMIT \_ changed 事件向音频堆栈表明音频设备的音频音量级别限制已更改。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespan-usage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span> 使用情况摘要表

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
<td align="left"><p><a href="/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的事件值类型是一个指定要用于此事件的通知方法的 **KSEVENTDATA** 结构。

<a name="remarks"></a>备注
-------

有关如何实现对 KSEVENT PINCAPS VOLUMELIMITCHANGE 事件的支持的信息 \_ \_ ，请参阅[**KSEVENT \_ PINCAPS \_ FORMATCHANGE**](ksevent-pincaps-formatchange.md)的 "**备注**" 部分。

请注意，虽然 KSEVENT \_ PINCAPS \_ FORMATCHANGE 是在链接到 Portcls) 的微型端口驱动程序 (上实现的，但 KSEVENT \_ VOLUMELIMIT \_ CHANGED 事件是在拓扑筛选器上实现的。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSEVENT**](/previous-versions/ff561744(v=vs.85))

[**KSEVENT \_ PINCAPS \_ FORMATCHANGE**](ksevent-pincaps-formatchange.md)

[**KSEVENTDATA**](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

