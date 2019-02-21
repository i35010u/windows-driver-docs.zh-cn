---
title: KSPROPERTY\_HRTF3D\_FILTER\_FORMAT
description: KSPROPERTY\_HRTF3D\_筛选器\_格式属性检索 HRTF 算法所用的筛选器格式。
ms.assetid: 7e4e869e-60ae-4266-93e4-0b6118951417
keywords:
- KSPROPERTY_HRTF3D_FILTER_FORMAT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_HRTF3D_FILTER_FORMAT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50b4383dd1a71145a4d0df6a1cd51efd887db3f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543364"
---
# <a name="kspropertyhrtf3dfilterformat"></a>KSPROPERTY\_HRTF3D\_FILTER\_FORMAT


KSPROPERTY\_HRTF3D\_筛选器\_格式属性检索 HRTF 算法所用的筛选器格式。

## <span id="ddk_ksproperty_hrtf3d_filter_format_ks"></span><span id="DDK_KSPROPERTY_HRTF3D_FILTER_FORMAT_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537104" data-raw-source="[&lt;strong&gt;KSDS3D_HRTF_FILTER_FORMAT_MSG&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537104)"><strong>KSDS3D_HRTF_FILTER_FORMAT_MSG</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种结构的类型 KSDS3D\_HRTF\_筛选器\_格式\_指定 HRTF 算法的筛选器方法和系数格式的消息。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_HRTF3D\_筛选器\_格式属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSDS3D\_HRTF\_FILTER\_FORMAT\_MSG**](https://msdn.microsoft.com/library/windows/hardware/ff537104)

 

 






