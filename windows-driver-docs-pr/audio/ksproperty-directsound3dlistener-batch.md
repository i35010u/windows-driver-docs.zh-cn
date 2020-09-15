---
title: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 批处理
description: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ batch 属性指定3d 侦听器的批处理模式设置。
ms.assetid: 370191f8-e5a2-40f0-a979-c14cf7f44756
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4955c34cf0320b7b3c650bf327fb95e2b97677e3
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102540"
---
# <a name="ksproperty_directsound3dlistener_batch"></a>KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 批处理


KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ batch 属性指定3d 侦听器的批处理模式设置。

## <span id="ddk_ksproperty_directsound3dlistener_batch_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_BATCH_KS"></span>


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
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

操作数据) 的属性值 (为 BOOL 类型并指定批处理模式设置：

-   如果此属性的值为 **TRUE**，则微型端口驱动程序应缓存对侦听器属性和所有关联的缓冲区属性所做的所有更改。

-   如果该值为 **FALSE**，则对侦听器属性和缓冲区属性所做的更改将立即生效。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 批属性请求返回状态 " \_ 成功" 以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

当此属性从 **TRUE** 转换为 **FALSE** 时，微型端口驱动程序应将所有缓存的属性立即生效。 如果可能，所有缓存的属性都应同时生效。

有关3D 侦听器的批处理模式设置的详细信息，请参阅 Microsoft Windows SDK 文档中的 **IDirectSound3DListener：： CommitDeferredSettings** 方法说明。

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

