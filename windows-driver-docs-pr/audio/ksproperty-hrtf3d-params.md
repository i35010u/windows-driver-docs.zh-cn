---
title: KSPROPERTY \_ HRTF3D \_ 参数
description: KSPROPERTY \_ HRTF3D \_ PARAMS 属性将一组3-d 参数值应用于 HRTF 算法。
ms.assetid: f7a7cfa9-de76-418a-be84-2519de454c89
keywords:
- KSPROPERTY_HRTF3D_PARAMS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_HRTF3D_PARAMS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b61a81bfe464565ee3c5532fa003f6b95f4fa81
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210977"
---
# <a name="ksproperty_hrtf3d_params"></a>KSPROPERTY \_ HRTF3D \_ 参数


KSPROPERTY \_ HRTF3D \_ PARAMS 属性将一组3-d 参数值应用于 HRTF 算法。

## <span id="ddk_ksproperty_hrtf3d_params_ks"></span><span id="DDK_KSPROPERTY_HRTF3D_PARAMS_KS"></span>


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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_params_msg" data-raw-source="[&lt;strong&gt;KSDS3D_HRTF_PARAMS_MSG&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_params_msg)"><strong>KSDS3D_HRTF_PARAMS_MSG</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是 \_ \_ 指定参数值的 KSDS3D HRTF PARAMS MSG 类型的结构 \_ 。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ HRTF3D \_ PARAMS 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

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
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSDS3D \_ HRTF \_ PARAMS \_ MSG**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_params_msg)

 

