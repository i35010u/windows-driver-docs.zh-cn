---
title: KSPROPERTY\_AUDIO\_AGC
description: KSPROPERTY\_音频\_AGC 属性 AGC 节点中指定的通道 AGC （自动增益控制） 的状态 (KSNODETYPE\_AGC)。
ms.assetid: 72630e9b-a1e7-4319-831a-94f8b856cf93
keywords:
- KSPROPERTY_AUDIO_AGC 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_AGC
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9613314a1a499a2c83f647d39ea3e6e2cbb77dc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576883"
---
# <a name="kspropertyaudioagc"></a>KSPROPERTY\_AUDIO\_AGC


KSPROPERTY\_音频\_AGC 属性 AGC 节点中指定的通道 AGC （自动增益控制） 的状态 ([**KSNODETYPE\_AGC**](ksnodetype-agc.md))。

## <span id="ddk_ksproperty_audio_agc_ks"></span><span id="DDK_KSPROPERTY_AUDIO_AGC_KS"></span>


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
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值属于类型 BOOL，指示 AGC 打开或关闭。 值为 **，则返回 TRUE**指示 AGC 上。 **FALSE**指示它已关闭。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_AGC 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

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


[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSNODETYPE\_AGC**](ksnodetype-agc.md)

 

 






