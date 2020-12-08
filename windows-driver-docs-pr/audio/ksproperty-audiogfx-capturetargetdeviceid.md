---
title: KSPROPERTY \_ AUDIOGFX \_ CAPTURETARGETDEVICEID
description: KSPROPERTY \_ AUDIOGFX \_ CAPTURETARGETDEVICEID 属性用于向 GFX 筛选器发出捕获流源音频设备的即插即用设备 ID。
keywords:
- KSPROPERTY_AUDIOGFX_CAPTURETARGETDEVICEID 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOGFX_CAPTURETARGETDEVICEID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84c37ec6f78ecb129457a40bf7e889c587a5dc53
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784423"
---
# <a name="ksproperty_audiogfx_capturetargetdeviceid"></a>KSPROPERTY \_ AUDIOGFX \_ CAPTURETARGETDEVICEID


KSPROPERTY \_ AUDIOGFX \_ CAPTURETARGETDEVICEID 属性用于向 GFX 筛选器发出捕获流源音频设备的即插即用设备 ID。

## <span id="ddk_ksproperty_audiogfx_capturetargetdeviceid_ks"></span><span id="DDK_KSPROPERTY_AUDIOGFX_CAPTURETARGETDEVICEID_KS"></span>


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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>WCHAR 数组</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是包含设备 ID 的 WCHAR 数组。 设备 ID 是以 null 结尾的 Unicode 字符字符串。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ AUDIOGFX \_ CAPTURETARGETDEVICEID 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此仅限集的属性请求的目标是一个 GFX 筛选器，该筛选器配置为用作捕获或呈现/捕获-GFX 筛选器。

若要确定保存属性值所需的缓冲区大小，请参阅 [音频属性的基本支持查询](./basic-support-queries-for-audio-properties.md)。

有关设备 Id 的其他信息，请参阅 [设备标识字符串](../install/device-identification-strings.md)。

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


[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

