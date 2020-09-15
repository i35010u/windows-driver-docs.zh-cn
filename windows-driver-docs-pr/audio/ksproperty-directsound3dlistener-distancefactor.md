---
title: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DISTANCEFACTOR
description: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DISTANCEFACTOR 属性指定应应用于任何距离值的距离系数。
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
ms.openlocfilehash: efa5ecff2a50de804cfc119fa01c0d563feb6136
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102536"
---
# <a name="ksproperty_directsound3dlistener_distancefactor"></a>KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DISTANCEFACTOR


KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DISTANCEFACTOR 属性指定应应用于任何距离值的距离系数。

## <span id="ddk_ksproperty_directsound3dlistener_distancefactor_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_DISTANCEFACTOR_KS"></span>


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
<th align="left">获取</th>
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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>FLOAT</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 FLOAT 类型并指定距离系数。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DISTANCEFACTOR 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

KSPROPSETID \_ DirectSound3DBuffer 和 KSPROPSETID DirectSound3DListener 属性的距离以 \_ 米倍于距离系数的单位表示。

默认情况下，距离系数为1，因此以米为单位表示距离。  (也是默认速度单位为每秒计量数。 ) 

客户端可以通过发送 KSPROPERTY DirectSound3DListener DISTANCEFACTOR ** \_ DirectSound3DBuffer** 请求指定不同的距离系数来更改 KSPROPSETID 和 **KSPROPSETID \_ DirectSound3DListener** 属性的距离单位 \_ \_ 。

DirectSound 使用此属性实现 **IDirectSound3DListener：： GetDistanceFactor** 和 **IDirectSound3DListener：： SetDistanceFactor** 方法，如 Microsoft Windows SDK 文档中所述。

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
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

