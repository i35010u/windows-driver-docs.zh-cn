---
title: KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME
description: KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME 属性指定的三维声音缓冲区圆锥体外部音量。
ms.assetid: faaa4419-6de4-4417-a9a6-922e60130946
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c6b2cd682e857fb3f902bbc7e5b3b03c5e87579
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332777"
---
# <a name="kspropertydirectsound3dbufferconeoutsidevolume"></a>KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME


KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME 属性指定的三维声音缓冲区圆锥体外部音量。

## <span id="ddk_ksproperty_directsound3dbuffer_coneoutsidevolume_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_CONEOUTSIDEVOLUME_KS"></span>


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
<td align="left"><p>长</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值的类型 long 类型的值，并指定圆锥体外部音量级别。 卷级别的 1/100ths 的分贝为单位表示。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DBUFFER\_CONEOUTSIDEVOLUME 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 3D 缓冲区圆锥体外部音量的详细信息，请参阅 Microsoft Windows SDK 文档中的以下：

-   **LConeOutsideVolume** DS3DBUFFER 结构中的成员。

-   **IDirectSound3DBuffer::GetOutsideVolume**并**IDirectSound3DBuffer::SetOutsideVolume**方法。

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

 

 






