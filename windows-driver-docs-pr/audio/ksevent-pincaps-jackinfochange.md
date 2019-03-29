---
title: KSEVENT\_PINCAPS\_JACKINFOCHANGE
description: KSEVENT\_PINCAPS\_JACKINFOCHANGE 事件指示音频堆栈为音频设备的插孔信息已更改。
ms.assetid: 46514043-5044-4373-94ca-b00898aeefba
keywords:
- KSEVENT_PINCAPS_JACKINFOCHANGE 音频设备
topic_type:
- apiref
api_name:
- KSEVENT_PINCAPS_JACKINFOCHANGE
api_location:
- Ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7289f5dcebb1d4b1fa0db26bbe8470f4bd9aa35f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566610"
---
# <a name="kseventpincapsjackinfochange"></a>KSEVENT\_PINCAPS\_JACKINFOCHANGE


`KSEVENT_PINCAPS_JACKINFOCHANGE`事件指示音频堆栈为音频设备的插孔信息已更改。

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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561744" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561744)"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

事件值类型 （操作数据） 是**KSEVENTDATA**结构，它指定要使用此事件的通知方法。

<a name="remarks"></a>备注
-------

有关如何实现对的支持信息`KSEVENT_PINCAPS_JACKINFOCHANGE`事件，请参阅备注部分[ **KSEVENT\_PINCAPS\_格式**](ksevent-pincaps-formatchange.md)主题。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSEVENT**](https://msdn.microsoft.com/library/windows/hardware/ff561744)

[**KSEVENTDATA**](https://msdn.microsoft.com/library/windows/hardware/ff561750)

[**KSEVENT\_PINCAPS\_格式**](ksevent-pincaps-formatchange.md)

 

 






