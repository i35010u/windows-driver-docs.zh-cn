---
title: KSPROPERTY\_AUDIOGFX\_CAPTURETARGETDEVICEID
description: KSPROPERTY\_AUDIOGFX\_CAPTURETARGETDEVICEID 属性用来通知是捕获流的源的音频设备的即插设备 ID 的 GFX 筛选器。
ms.assetid: df4505c5-f9ff-4f8a-8521-90031c0b23e4
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
ms.openlocfilehash: f166b84eb9c00b3ae4fb289e6f84f7d8150637e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332785"
---
# <a name="kspropertyaudiogfxcapturetargetdeviceid"></a>KSPROPERTY\_AUDIOGFX\_CAPTURETARGETDEVICEID


KSPROPERTY\_AUDIOGFX\_CAPTURETARGETDEVICEID 属性用来通知是捕获流的源的音频设备的即插设备 ID 的 GFX 筛选器。

## <span id="ddk_ksproperty_audiogfx_capturetargetdeviceid_ks"></span><span id="DDK_KSPROPERTY_AUDIOGFX_CAPTURETARGETDEVICEID_KS"></span>


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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>WCHAR 数组</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个 WCHAR 数组，其中包含设备 id。 设备 ID 是以 null 结尾的 Unicode 字符的字符串。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AUDIOGFX\_CAPTURETARGETDEVICEID 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此设置只读属性，请求的目标是 GFX 筛选器配置用作是捕获或呈现/捕获 GFX 筛选器。

若要确定保存属性值所需的缓冲区的大小，请参阅[音频属性的基本支持查询](https://msdn.microsoft.com/library/windows/hardware/ff536225)。

有关设备 Id 的其他信息，请参阅[设备标识字符串](https://msdn.microsoft.com/library/windows/hardware/ff541224)。

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

 

 






