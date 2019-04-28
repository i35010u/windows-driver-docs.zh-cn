---
title: KSPROPERTY\_SOUNDDETECTOR\_ARMED
description: KSPROPERTY\_SOUNDDETECTOR\_臂的属性是检测程序的当前 arming 状态。
ms.assetid: 3B9B43C0-31EE-4490-AD29-98DA81D1664F
keywords:
- KSPROPERTY_SOUNDDETECTOR_ARMED 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_ARMED
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce1c9e03026548fcfec933dc0bfd6a7c940a0d1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332642"
---
# <a name="kspropertysounddetectorarmed"></a>KSPROPERTY\_SOUNDDETECTOR\_ARMED


**KSPROPERTY\_SOUNDDETECTOR\_ARMED**属性是检测程序的当前 arming 状态。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

属性值为布尔值，指示 arming 检测程序的状态。

<a name="remarks"></a>备注
-------

操作系统将此上限设置为 true，则加入检测程序。

该驱动程序将此重置为 false:

-   禁用筛选器接口。
-   [ **KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)属性设置。
-   检测到一个关键字。

虽然没有关键字的模式下将设置此 true ([**KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)为空) 不起作用。
&gt; \[!请注意\]&gt;此属性为 true，则随后设置[ **KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)会自动重置为false，如前面所述。

 

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


[**KSPROPERTY\_SOUNDDETECTOR\_模式**](ksproperty-sounddetector-patterns.md)

[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

 

 






