---
title: KSPROPERTY\_HRTF3D\_\_格式的筛选器
description: KSPROPERTY\_HRTF3D\_FILTER\_FORMAT 属性检索 HRTF 算法使用的筛选器格式。
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
ms.openlocfilehash: df2107db2b2940ae8dc265d9de5d017d87a9422e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830707"
---
# <a name="ksproperty_hrtf3d_filter_format"></a>KSPROPERTY\_HRTF3D\_\_格式的筛选器


KSPROPERTY\_HRTF3D\_FILTER\_FORMAT 属性检索 HRTF 算法使用的筛选器格式。

## <span id="ddk_ksproperty_hrtf3d_filter_format_ks"></span><span id="DDK_KSPROPERTY_HRTF3D_FILTER_FORMAT_KS"></span>


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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_filter_format_msg" data-raw-source="[&lt;strong&gt;KSDS3D_HRTF_FILTER_FORMAT_MSG&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_filter_format_msg)"><strong>KSDS3D_HRTF_FILTER_FORMAT_MSG</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是 KSDS3D\_HRTF 类型的结构\_筛选器\_格式\_消息，用于指定 HRTF 算法的筛选方法和系数格式。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_HRTF3D\_FILTER\_格式属性请求返回状态\_"成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSDS3D\_HRTF\_筛选\_格式\_消息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_hrtf_filter_format_msg)

 

 






