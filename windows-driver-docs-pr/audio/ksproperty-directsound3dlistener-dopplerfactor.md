---
title: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DOPPLERFACTOR
description: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DOPPLERFACTOR 属性指定3d 侦听器的 Doppler 系数。
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
ms.openlocfilehash: a563b5b82351e234c8e22d3e450d188e770ad76e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208923"
---
# <a name="ksproperty_directsound3dlistener_dopplerfactor"></a>KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DOPPLERFACTOR


KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DOPPLERFACTOR 属性指定3d 侦听器的 Doppler 系数。

## <span id="ddk_ksproperty_directsound3dlistener_dopplerfactor_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_DOPPLERFACTOR_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>FLOAT</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 FLOAT 类型，并指定 Doppler 系数。 Doppler 因子的范围可以是从 DS3D \_ MINDOPPLERFACTOR 到 DS3D \_ MAXDOPPLERFACTOR，它们分别定义为0.0 和10.0。 默认系数为 DS3D \_ DEFAULTDOPPLERFACTOR，其定义为1.0。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DOPPLERFACTOR 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性指定应用于3D 侦听器和3D 声音缓冲区的 Doppler 系数。

如果 Doppler 因子为零，则表示无论侦听器或声音缓冲区的速度如何，都不会将 Doppler 移动应用到声音。 大于1的系数夸大将在现实世界中发生的 Doppler 偏移量。

DirectSound 使用此属性实现 **IDirectSound3DListener：： GetDopplerFactor** 和 **IDirectSound3DListener：： SetDopplerFactor** 方法，如 Microsoft Windows SDK 文档中所述。

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

 

