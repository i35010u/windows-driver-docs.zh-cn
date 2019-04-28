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
ms.openlocfilehash: ddb5b21b1a7b8d8c341092def2c9b35e6fd248b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333338"
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561744" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561744)"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

事件值类型 （操作数据） 是**KSEVENTDATA**结构，它指定要使用此事件的通知方法。

<a name="remarks"></a>备注
-------

有关如何实现对 KSEVENT 的支持信息\_PINCAPS\_VOLUMELIMITCHANGE 事件，请参阅**备注**一部分[ **KSEVENT\_PINCAPS\_格式**](ksevent-pincaps-formatchange.md)。

请注意，尽管 KSEVENT\_PINCAPS\_格式批筛选器 （用于微型端口驱动程序链接到 Portcls），通过实现 KSEVENT\_VOLUMELIMIT\_在拓扑上实现已更改事件筛选器。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSEVENT**](https://msdn.microsoft.com/library/windows/hardware/ff561744)

[**KSEVENT\_PINCAPS\_格式**](ksevent-pincaps-formatchange.md)

[**KSEVENTDATA**](https://msdn.microsoft.com/library/windows/hardware/ff561750)

 

 






