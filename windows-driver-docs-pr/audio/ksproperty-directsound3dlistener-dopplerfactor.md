---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_DOPPLERFACTOR
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_DOPPLERFACTOR 属性指定三维侦听器 Doppler 身份。
ms.assetid: e07eb51f-6d87-4183-90cc-09bfa7523944
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 263df085ca0875808cb165bd75bcad3a6ec96c80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555810"
---
# <a name="kspropertydirectsound3dlistenerdopplerfactor"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_DOPPLERFACTOR


KSPROPERTY\_DIRECTSOUND3DLISTENER\_DOPPLERFACTOR 属性指定三维侦听器 Doppler 身份。

## <span id="ddk_ksproperty_directsound3dlistener_dopplerfactor_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR_KS"></span>


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
<td align="left"><p>浮点数</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值类型为 FLOAT 的是，它指定 Doppler 身份。 Doppler 身份可以介于 DS3D\_MINDOPPLERFACTOR 到 DS3D\_MAXDOPPLERFACTOR，分别定义为介于 0.0 和 10.0。 默认因素是 DS3D\_DEFAULTDOPPLERFACTOR，定义为 1.0。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DLISTENER\_DOPPLERFACTOR 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性指定应用于三维侦听器和 3D 声音缓冲区的 Doppler 因素。

零的 Doppler 因素意味着没有 Doppler shift 应用于声音而不考虑侦听器或声音缓冲区的速度。 大于 1 的因素夸大 Doppler 转变，这会在现实生活中发生的量。

DirectSound 使用此属性来实现**IDirectSound3DListener::GetDopplerFactor**并**IDirectSound3DListener::SetDopplerFactor** Microsoft 所述的方法Windows SDK 文档。

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

 

 






