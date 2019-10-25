---
title: KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES
description: KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES 属性指定3D 声音缓冲区的声音投影圆锥的内部和外部锥角。
ms.assetid: a3978aaf-218c-4021-abf0-e426eacf52c7
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc8a90a0cf85323d1f3c1d28dacb8b5847157b0a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832836"
---
# <a name="ksproperty_directsound3dbuffer_coneangles"></a>KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES


KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES 属性指定3D 声音缓冲区的声音投影圆锥的内部和外部锥角。

## <span id="ddk_ksproperty_directsound3dbuffer_coneangles_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES_KS"></span>


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
<td align="left"><p>“是”</p></td>
<td align="left"><p>大头针</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_cone_angles" data-raw-source="[&lt;strong&gt;KSDS3D_BUFFER_CONE_ANGLES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_cone_angles)"><strong>KSDS3D_BUFFER_CONE_ANGLES</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一种类型为 KSDS3D\_BUFFER 的结构\_圆锥\_角，用于指定锥角和外侧。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES 属性请求返回状态\_SUCCESS，以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

若要详细了解 DirectSound 3D 缓冲区的声音投影圆锥的内部和外部锥角，请参阅 Microsoft Windows SDK 文档中的以下内容：

-   DS3DBUFFER 结构的**dwInsideConeAngle**和**dwOutsideConeAngle**成员。

-   **IDirectSound3DBuffer：： GetConeAngles**和**IDirectSound3DBuffer：： SetConeAngles**方法。

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

[**KSDS3D\_BUFFER\_圆锥\_角度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_cone_angles)

 

 






