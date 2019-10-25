---
title: KSPROPERTY\_DIRECTSOUND3DLISTENER\_方向
description: KSPROPERTY\_DIRECTSOUND3DLISTENER\_方向属性指定3D 侦听器的方向。
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
ms.openlocfilehash: 13388615d98d033af75eb6cdeab58026e27e175a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832809"
---
# <a name="ksproperty_directsound3dlistener_orientation"></a>KSPROPERTY\_DIRECTSOUND3DLISTENER\_方向


KSPROPERTY\_DIRECTSOUND3DLISTENER\_方向属性指定3D 侦听器的方向。

## <span id="ddk_ksproperty_directsound3dlistener_orientation_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ORIENTATION_KS"></span>


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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>“是”</p></td>
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_orientation" data-raw-source="[&lt;strong&gt;KSDS3D_LISTENER_ORIENTATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_orientation)"><strong>KSDS3D_LISTENER_ORIENTATION</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定侦听器方向的 KSDS3D\_侦听器\_方向的结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_DIRECTSOUND3DLISTENER\_方向属性请求返回状态\_SUCCESS，指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

DirectSound 使用此属性实现**IDirectSound3DListener：： GetOrientation**和**IDirectSound3DListener：： SetOrientation**方法，如 Microsoft Windows SDK 文档中所述。

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSDS3D\_侦听器\_方向**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_listener_orientation)

 

 






