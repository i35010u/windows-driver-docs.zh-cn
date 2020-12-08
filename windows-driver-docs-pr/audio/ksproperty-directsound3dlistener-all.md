---
title: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ ALL
description: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ all 属性用于设置或获取指定侦听器 ID 的所有 DirectSound 3d 侦听器属性。
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
ms.openlocfilehash: e40231ea3e5aabe7b53d2a61f415d8f297735621
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798893"
---
# <a name="ksproperty_directsound3dlistener_all"></a>KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ ALL


KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ all 属性用于设置或获取指定侦听器 ID 的所有 DirectSound 3d 侦听器属性。

## <span id="ddk_ksproperty_directsound3dlistener_all_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ALL_KS"></span>


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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_all" data-raw-source="[&lt;strong&gt;KSDS3D_LISTENER_ALL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_all)"><strong>KSDS3D_LISTENER_ALL</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSDS3D 侦听器类型的 \_ 结构 \_ ，该结构指定3d 侦听器的所有属性。 此结构类似于 DS3DBUFFER 结构，如 Microsoft Windows SDK 文档中所述。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ ALL 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 使用此属性实现 **IDirectSound3DBuffer：： GetAllParameters** 和 **IDirectSound3DBuffer：： SetAllParameters** 方法，如 Windows SDK 文档中所述。

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

[**\_全部 KSDS3D 侦听器 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_all)

