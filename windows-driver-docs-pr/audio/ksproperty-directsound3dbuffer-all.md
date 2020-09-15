---
title: KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ ALL
description: KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ all 属性用于获取或设置指定缓冲区的所有 DirectSound 3d 缓冲区属性。
ms.assetid: 7c62a0f2-080b-42cd-a30e-7ceb5edad894
keywords:
- KSPROPERTY_DIRECTSOUND3DBUFFER_ALL 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DBUFFER_ALL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29a83ce814d10d6e841efdc0b42f66bc340fe26a
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102588"
---
# <a name="ksproperty_directsound3dbuffer_all"></a>KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ ALL


KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ all 属性用于获取或设置指定缓冲区的所有 DirectSound 3d 缓冲区属性。

## <span id="ddk_ksproperty_directsound3dbuffer_all_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DBUFFER_ALL_KS"></span>


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
<td align="left"><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_all" data-raw-source="[&lt;strong&gt;KSDS3D_BUFFER_ALL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_all)"><strong>KSDS3D_BUFFER_ALL</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSDS3D buffer 类型的 \_ 结构 \_ ，它指定了缓冲区的3d 特性。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ DIRECTSOUND3DBUFFER \_ ALL 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

KSDS3D \_ BUFFER \_ ALL 结构类似于在 Microsoft Windows SDK 文档中介绍的 DS3DBUFFER 结构。

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

[**KSDS3D \_ BUFFER \_ ALL**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_buffer_all)

