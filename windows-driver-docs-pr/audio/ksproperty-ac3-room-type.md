---
title: KSPROPERTY\_AC3\_ROOM\_TYPE
description: KSPROPERTY\_AC3\_聊天室\_类型属性指定的类型和在其中生成最终的音频会话混合聊天室的校准。
ms.assetid: 4e160fda-01f2-4517-bbc3-a9ae5b19f6c2
keywords:
- KSPROPERTY_AC3_ROOM_TYPE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_ROOM_TYPE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bb838f6924969759e9a52e37e418c3bdee06fc4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333098"
---
# <a name="kspropertyac3roomtype"></a>KSPROPERTY\_AC3\_ROOM\_TYPE


KSPROPERTY\_AC3\_聊天室\_类型属性指定的类型和在其中生成最终的音频会话混合聊天室的校准。

## <span id="ddk_ksproperty_ac3_room_type_ks"></span><span id="DDK_KSPROPERTY_AC3_ROOM_TYPE_KS"></span>


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
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537082" data-raw-source="[&lt;strong&gt;KSAC3_ROOM_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537082)"><strong>KSAC3_ROOM_TYPE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSAC3\_聊天室\_类型结构，它指定混合在其中生成 AC-3 编码流的空间的类型。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AC3\_聊天室\_类型属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性提供有关 AC-3 编码流的生产环境的信息。 属性值通常不由 ac-3 解码器，但可能由其他音频组件。

如果已编码的流未指定的空间类型，属性请求将返回错误代码。

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

[**KSAC3\_ROOM\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/ff537082)

 

 






