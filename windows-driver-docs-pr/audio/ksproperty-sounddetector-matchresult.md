---
title: KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT
description: KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT 属性包含匹配项的结果数据。
ms.assetid: A4CDE539-3C99-4E66-B678-AF56BFFEE460
keywords:
- KSPROPERTY_SOUNDDETECTOR_MATCHRESULT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_MATCHRESULT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a617564ad5c9a50d78e1581dd6c6107403239ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332638"
---
# <a name="kspropertysounddetectormatchresult"></a>KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT


**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**属性包含匹配项的结果数据。

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
<td align="left"><p>否</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn957513" data-raw-source="[&lt;strong&gt;SOUNDDETECTOR_PATTERNHEADER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn957513)"><strong>SOUNDDETECTOR_PATTERNHEADER</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

一个[ **SOUNDDETECTOR\_PATTERNHEADER** ](https://msdn.microsoft.com/library/windows/hardware/dn957513)结构后, 跟结果数据负载。

<a name="remarks"></a>备注
-------

结果数据包括[ **SOUNDDETECTOR\_PATTERNHEADER** ](https://msdn.microsoft.com/library/windows/hardware/dn957513)识别结果数据，以及 OEMDLLCOM 对象来处理结果数据的格式。

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


[**SOUNDDETECTOR\_PATTERNHEADER**](https://msdn.microsoft.com/library/windows/hardware/dn957513)

[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

 

 






