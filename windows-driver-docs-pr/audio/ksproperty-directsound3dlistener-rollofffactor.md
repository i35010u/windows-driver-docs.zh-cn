---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR 属性指定三维侦听器卷绕身份。
ms.assetid: 3eef80ef-921b-4364-b31d-14a62f305f5d
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c575914f63950f425c67a28144decd3020172c33
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361010"
---
# <a name="kspropertydirectsound3dlistenerrollofffactor"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR


KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR 属性指定三维侦听器卷绕身份。

## <span id="ddk_ksproperty_directsound3dlistener_rollofffactor_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>浮点数</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值类型为 FLOAT 的是，它指定卷绕身份。 卷绕身份可以介于 DS3D\_MINROLLOFFFACTOR 到 DS3D\_MAXROLLOFFFACTOR，分别定义为介于 0.0 和 10.0。 默认卷绕因素是 DS3D\_DEFAULTROLLOFFFACTOR，定义为 1.0。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DLISTENER\_ROLLOFFFACTOR 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

卷绕是衰减的应用于声音，基于声音的源的侦听器的距离量。 卷绕因子为零意味着从侦听器没有衰减应用于声音而不考虑其距离。 大于 1 的因素夸大声音与距离的实际衰减。

DirectSound 使用此属性来实现**IDirectSound3DListener::GetRolloffFactor**并**IDirectSound3DListener::SetRolloffFactor** Microsoft 所述的方法Windows SDK 文档。

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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

 

 






