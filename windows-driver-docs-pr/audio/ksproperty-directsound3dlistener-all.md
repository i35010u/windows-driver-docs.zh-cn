---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_所有
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_所有属性都用于设置或获取指定的侦听器 ID DirectSound 3D 侦听器的所有属性
ms.assetid: cdf98ed6-cd8e-480c-b766-c348f41919ef
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ALL 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ALL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64b067aca3265c18f1dec8a692a449f6c92cc077
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332800"
---
# <a name="kspropertydirectsound3dlistenerall"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_所有


KSPROPERTY\_DIRECTSOUND3DLISTENER\_所有属性都用于设置或获取指定的侦听器 ID DirectSound 3D 侦听器的所有属性

## <span id="ddk_ksproperty_directsound3dlistener_all_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ALL_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537116" data-raw-source="[&lt;strong&gt;KSDS3D_LISTENER_ALL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537116)"><strong>KSDS3D_LISTENER_ALL</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种结构的类型 KSDS3D\_侦听器\_所有指定的三维侦听器的所有属性。 此结构是类似于 DS3DBUFFER 结构，它 Microsoft Windows SDK 文档中所述。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DLISTENER\_所有属性请求将都返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 使用此属性来实现**IDirectSound3DBuffer::GetAllParameters**并**IDirectSound3DBuffer::SetAllParameters** Windows SDK 中介绍的方法文档。

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

[**KSDS3D\_LISTENER\_ALL**](https://msdn.microsoft.com/library/windows/hardware/ff537116)

 

 






