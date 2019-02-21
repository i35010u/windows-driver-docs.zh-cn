---
title: KSPROPERTY\_AUDIO\_MUX\_SOURCE
description: KSPROPERTY\_音频\_MUX\_源属性指定的输出流的多路复用器的源。 这是 MUX 节点的属性 (KSNODETYPE\_MUX)。
ms.assetid: 631d12f2-3f30-4d3e-a0b2-731634858897
keywords:
- KSPROPERTY_AUDIO_MUX_SOURCE Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MUX_SOURCE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8454969ac993c5dbb9d41526bc920688aa37109c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543504"
---
# <a name="kspropertyaudiomuxsource"></a>KSPROPERTY\_AUDIO\_MUX\_SOURCE


KSPROPERTY\_音频\_MUX\_源属性指定的输出流的多路复用器的源。 这是 MUX 节点的属性 ([**KSNODETYPE\_MUX**](ksnodetype-mux.md))。

## <span id="ddk_ksproperty_audio_mux_source_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MUX_SOURCE_KS"></span>


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
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

类型为 ULONG 是属性值 （操作数据）。 此值是 MUX 节点上的所选输入 pin 的 pin ID。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_MUX\_源属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

Pin ID 标识逻辑 pin MUX 节点上。 在筛选器节点上的逻辑 pin 的 pin Id 的讨论，请参阅[ **PCCONNECTION\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537688)。

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
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODETYPE\_MUX**](ksnodetype-mux.md)

[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**PCCONNECTION\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537688)

 

 






