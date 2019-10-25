---
title: KSEVENT\_PINCAPS\_JACKINFOCHANGE
description: KSEVENT\_PINCAPS\_JACKINFOCHANGE 事件向音频堆栈表明音频设备的插孔信息已更改。
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
ms.openlocfilehash: 995ad652db0d56fb71c1fb514b5e9ecfe868b12d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833120"
---
# <a name="ksevent_pincaps_jackinfochange"></a>KSEVENT\_PINCAPS\_JACKINFOCHANGE


`KSEVENT_PINCAPS_JACKINFOCHANGE` 事件向音频堆栈表明音频设备的插孔信息已更改。

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
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

事件值类型（操作数据）是指定要用于此事件的通知方法的**KSEVENTDATA**结构。

<a name="remarks"></a>备注
-------

有关如何实现 `KSEVENT_PINCAPS_JACKINFOCHANGE` 事件支持的信息，请参阅[**KSEVENT\_PINCAPS\_FORMATCHANGE**](ksevent-pincaps-formatchange.md)的 "备注" 部分。

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
<td align="left"><p>在 windows 7 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

[**KSEVENT\_PINCAPS\_FORMATCHANGE**](ksevent-pincaps-formatchange.md)

 

 






