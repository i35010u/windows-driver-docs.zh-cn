---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR 属性指定应应用于任何距离值的距离因素。
ms.assetid: 38daa5d8-d70f-4484-bf5a-a9a365296313
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fe6dfe30ade6190f2056c5a5f753533192a4458
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360549"
---
# <a name="kspropertydirectsound3dlistenerdistancefactor"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR


KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR 属性指定应应用于任何距离值的距离因素。

## <span id="ddk_ksproperty_directsound3dlistener_distancefactor_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR_KS"></span>


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

 

（操作数据） 的属性值类型为 FLOAT 的是，它指定距离身份。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

距离为 KSPROPSETID\_DirectSound3DBuffer 和 KSPROPSETID\_DirectSound3DListener 属性以计量距离身份时间的单位表示。

默认情况下，距离因子为 1，因此以米为单位表示的距离。 （此外，默认速度单位是米 / 秒。）

客户端可以更改的距离单位**KSPROPSETID\_DirectSound3DBuffer**并**KSPROPSETID\_DirectSound3DListener**通过发送 KSPROPERTY属性\_DIRECTSOUND3DLISTENER\_DISTANCEFACTOR 指定不同距离身份的组属性请求。

DirectSound 使用此属性来实现**IDirectSound3DListener::GetDistanceFactor**并**IDirectSound3DListener::SetDistanceFactor** Microsoft 所述的方法Windows SDK 文档。

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

 

 






