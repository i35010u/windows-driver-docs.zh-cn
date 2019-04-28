---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_速度
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_速度属性指定的三维侦听器速度向量。
ms.assetid: 654a8cd1-c8ad-4d65-9d14-7602d269bcff
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_VELOCITY Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_VELOCITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53c3b83153ea83cc2ea4b7e0c553d51bc88ab626
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332732"
---
# <a name="kspropertydirectsound3dlistenervelocity"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_速度


KSPROPERTY\_DIRECTSOUND3DLISTENER\_速度属性指定的三维侦听器速度向量。

## <span id="ddk_ksproperty_directsound3dlistener_velocity_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_VELOCITY_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff536367" data-raw-source="[&lt;strong&gt;DS3DVECTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536367)"><strong>DS3DVECTOR</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为类型指定速度向量的 DS3DVECTOR 的结构。 速度以每秒的距离单位表示。 默认距离单位是米。 可以通过发送更改距离单位[ **KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)集属性请求。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DLISTENER\_速度属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 使用此属性来实现**IDirectSound3DListener::GetVelocity**并**IDirectSound3DListener::SetVelocity** Microsoft Windows SDK 中介绍的方法文档。

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

[**DS3DVECTOR**](https://msdn.microsoft.com/library/windows/hardware/ff536367)

 

 






