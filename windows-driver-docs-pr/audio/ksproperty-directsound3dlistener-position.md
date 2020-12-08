---
title: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 位置
description: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ position 属性指定3d 侦听器的位置。
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_POSITION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6ad2f712326b2a0b79d35e2c84df657d8ae22fe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798877"
---
# <a name="ksproperty_directsound3dlistener_position"></a>KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 位置


KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ position 属性指定3d 侦听器的位置。

## <span id="ddk_ksproperty_directsound3dlistener_position_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_POSITION_KS"></span>


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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ds3dvector" data-raw-source="[&lt;strong&gt;DS3DVECTOR&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ds3dvector)"><strong>DS3DVECTOR</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是指定侦听器位置的 DS3DVECTOR 类型的结构。 位置坐标以当前距离单位表示。 有关距离单位的信息，请参阅 [**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ POSITION 属性请求返回状态 \_ SUCCESS 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 使用此属性实现 **IDirectSound3DListener：： GetPosition** 和 **IDirectSound3DListener：： SetPosition** 方法，如 Microsoft Windows SDK 文档中所述。

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

[**DS3DVECTOR**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ds3dvector)

[**KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ DISTANCEFACTOR**](ksproperty-directsound3dlistener-distancefactor.md)

