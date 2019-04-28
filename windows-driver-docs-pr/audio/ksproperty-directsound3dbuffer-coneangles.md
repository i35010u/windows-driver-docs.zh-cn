---
title: KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES
description: KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES 属性指定的内部和外部锥角 3D 声音缓冲区的声音投影圆锥。
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
ms.openlocfilehash: d38ac250b0408128ab139e29a6f88418fe6a75a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332764"
---
# <a name="kspropertydirectsound3dbufferconeangles"></a>KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES


KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES 属性指定的内部和外部锥角 3D 声音缓冲区的声音投影圆锥。

## <span id="ddk_ksproperty_directsound3dbuffer_coneangles_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_CONEANGLES_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537103" data-raw-source="[&lt;strong&gt;KSDS3D_BUFFER_CONE_ANGLES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537103)"><strong>KSDS3D_BUFFER_CONE_ANGLES</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种结构的类型 KSDS3D\_缓冲区\_圆锥体\_指定的内部和外部锥角的角度。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEANGLES 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

有关内部和外部锥角 DirectSound 3D 缓冲区声音投影圆锥体的详细信息，请参阅 Microsoft Windows SDK 文档中的以下：

-   **DwInsideConeAngle**并**dwOutsideConeAngle** DS3DBUFFER 结构的成员。

-   **IDirectSound3DBuffer::GetConeAngles**并**IDirectSound3DBuffer::SetConeAngles**方法。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSDS3D\_BUFFER\_CONE\_ANGLES**](https://msdn.microsoft.com/library/windows/hardware/ff537103)

 

 






