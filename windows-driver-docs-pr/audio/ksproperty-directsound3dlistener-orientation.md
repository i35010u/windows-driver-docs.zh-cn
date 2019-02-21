---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_方向
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_ORIENTATION 属性指定的三维侦听器的方向。
ms.assetid: 324b0def-e989-4dd1-9266-17d018dd512c
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ORIENTATION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ORIENTATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45b9d176ec3d33c90fdb590f2838bdea7a22c665
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548196"
---
# <a name="kspropertydirectsound3dlistenerorientation"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_方向


KSPROPERTY\_DIRECTSOUND3DLISTENER\_ORIENTATION 属性指定的三维侦听器的方向。

## <span id="ddk_ksproperty_directsound3dlistener_orientation_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ORIENTATION_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537119" data-raw-source="[&lt;strong&gt;KSDS3D_LISTENER_ORIENTATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537119)"><strong>KSDS3D_LISTENER_ORIENTATION</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种结构的类型 KSDS3D\_侦听器\_指定侦听器的方向的方向。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DLISTENER\_方向属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 使用此属性来实现**IDirectSound3DListener::GetOrientation**并**IDirectSound3DListener::SetOrientation** Microsoft Windows SDK 中介绍的方法文档。

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

[**KSDS3D\_LISTENER\_ORIENTATION**](https://msdn.microsoft.com/library/windows/hardware/ff537119)

 

 






