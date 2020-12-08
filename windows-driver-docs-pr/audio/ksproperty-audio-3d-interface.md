---
title: KSPROPERTY \_ AUDIO \_ 3d \_ 接口
description: KSPROPERTY \_ AUDIO \_ 3d \_ INTERFACE 属性指定用于处理声音缓冲区中的数据的3d 算法。
keywords:
- KSPROPERTY_AUDIO_3D_INTERFACE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_3D_INTERFACE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09852d90cca16e6f28d64f01584677f5a06a33bc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784559"
---
# <a name="ksproperty_audio_3d_interface"></a>KSPROPERTY \_ AUDIO \_ 3d \_ 接口


KSPROPERTY \_ AUDIO \_ 3d \_ INTERFACE 属性指定用于处理声音缓冲区中的数据的3d 算法。

## <span id="ddk_ksproperty_audio_3d_interface_ks"></span><span id="DDK_KSPROPERTY_AUDIO_3D_INTERFACE_KS"></span>


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
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是指定3D 算法的 GUID。 此值可以是头文件 Dsound 中的以下 Guid 之一：

-   DS3DALG \_ 默认值

-   DS3DALG \_ 无 \_ 虚拟化

-   DS3DALG \_ HRTF \_ FULL

-   DS3DALG \_ HRTF \_ 浅色

有关这些 Guid 的详细信息，请参阅 Microsoft Windows SDK 文档中的 DSBUFFERDESC 结构的 **guid3dAlgorithm** 成员的说明。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ AUDIO \_ 3d \_ 接口属性请求返回状态 " \_ 成功" 以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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

[**KSNODETYPE \_ 三维 \_ 效果**](ksnodetype-3d-effects.md)

