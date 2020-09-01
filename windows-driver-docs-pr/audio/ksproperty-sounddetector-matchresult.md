---
title: KSPROPERTY \_ SOUNDDETECTOR \_ MATCHRESULT
description: KSPROPERTY \_ SOUNDDETECTOR \_ MATCHRESULT 属性包含匹配项的结果数据。
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
ms.openlocfilehash: e264675bb22b5509169e4adde9ce3d4618109800
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210901"
---
# <a name="ksproperty_sounddetector_matchresult"></a>KSPROPERTY \_ SOUNDDETECTOR \_ MATCHRESULT


**KSPROPERTY \_ SOUNDDETECTOR \_ MATCHRESULT**属性包含匹配项的结果数据。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th align="left">获取</th>
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
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader" data-raw-source="[&lt;strong&gt;SOUNDDETECTOR_PATTERNHEADER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader)"><strong>SOUNDDETECTOR_PATTERNHEADER</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

后跟结果数据负载的 [**SOUNDDETECTOR \_ PATTERNHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader) 结构。

<a name="remarks"></a>备注
-------

结果数据包含 [**SOUNDDETECTOR \_ PATTERNHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader) ，用于标识结果数据的格式以及用于处理结果数据的 OEMDLLCOM 对象。

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
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**SOUNDDETECTOR \_ PATTERNHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader)

[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

 

