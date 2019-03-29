---
title: KSPROPERTY\_音频\_VOLUMELEVEL
description: KSPROPERTY\_音频\_VOLUMELEVEL 属性卷节点中指定的通道的卷级别 (KSNODETYPE\_卷)。
ms.assetid: 5b420c71-fc82-413d-a93d-e8f3408cc8d7
keywords:
- KSPROPERTY_AUDIO_VOLUMELEVEL 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_VOLUMELEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: af23b51c9564f0ca63bc4a2e3fb9701d683b9f72
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576852"
---
# <a name="kspropertyaudiovolumelevel"></a>KSPROPERTY\_音频\_VOLUMELEVEL


KSPROPERTY\_音频\_VOLUMELEVEL 属性卷节点中指定的通道的卷级别 ([**KSNODETYPE\_卷**](ksnodetype-volume.md))。

## <span id="ddk_ksproperty_audio_volumelevel_ks"></span><span id="DDK_KSPROPERTY_AUDIO_VOLUMELEVEL_KS"></span>


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
<td align="left"><p>通过筛选器或 Pin 实例的节点</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值属于类型长时间，在给定的流中指定的通道的卷级别。 音量级别值使用以下等级：

是-2147483648-无穷大分贝 （衰减）

在-2147483647 是-32767.99998474 分贝 （衰减） 和

+2147483647 是 +32767.99998474 分贝 （提升）。

&gt; \[!请注意\]&gt;分贝范围由整数值表示从-2147483648 到 +2147483647，其中此范围具有的分辨率为 1/65536 分贝。

 

如果超出范围的筛选器指定的值，则设置此属性的请求仍会成功。 仅可确定已应用于筛选器的实际值，但对此属性的后续 Get 调用。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_VOLUMELEVEL 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性的属性描述符指定频道号。 如果通过卷节点流中所包含*n*通道，通道是编号从的 0 到*n*-1。 有关详细信息，请参阅[公开多通道节点](https://msdn.microsoft.com/library/windows/hardware/ff536380)。

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


[自定义默认音频音量设置](https://msdn.microsoft.com/library/windows/hardware/jj870738)

[默认音频的音量设置](https://msdn.microsoft.com/library/windows/hardware/ff536251)

[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSNODETYPE\_卷**](ksnodetype-volume.md)

 

 






