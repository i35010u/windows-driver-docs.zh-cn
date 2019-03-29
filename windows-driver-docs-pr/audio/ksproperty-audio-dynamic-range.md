---
title: KSPROPERTY\_AUDIO\_DYNAMIC\_RANGE
description: KSPROPERTY\_音频\_动态\_范围属性指定是从响度节点的输出音频流的动态范围 (KSNODETYPE\_响度)。
ms.assetid: bab1cc2c-0751-4425-8546-9587baece585
keywords:
- KSPROPERTY_AUDIO_DYNAMIC_RANGE Audio Devices
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DYNAMIC_RANGE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1423d301b123deded0b7f0dc972049b770c085c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576841"
---
# <a name="kspropertyaudiodynamicrange"></a>KSPROPERTY\_AUDIO\_DYNAMIC\_RANGE


KSPROPERTY\_音频\_动态\_范围属性指定是从响度节点的输出音频流的动态范围 ([**KSNODETYPE\_响度**](ksnodetype-loudness.md)).

## <span id="ddk_ksproperty_audio_dynamic_range_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DYNAMIC_RANGE_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537085" data-raw-source="[&lt;strong&gt;KSAUDIO_DYNAMIC_RANGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537085)"><strong>KSAUDIO_DYNAMIC_RANGE</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一种结构的类型 KSAUDIO\_动态\_范围，它指定动态范围的响度节点的输出流。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_动态\_范围属性请求返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

默认情况下为值**QuietCompression**并**LoudCompression** KSAUDIO 成员\_动态\_范围结构设置为 0%。 这将产生的音频流的完整动态范围。 微型端口驱动程序将属性设置为其默认值时实例化的数据路径包含的节点的 pin。

某些设备可能不支持将变为**QuietCompression**并**LoudCompression**。 如果客户端尝试更改一个值，该设备不支持该值，微型端口驱动程序应返回错误。

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


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODETYPE\_响度**](ksnodetype-loudness.md)

[**KSAUDIO\_DYNAMIC\_RANGE**](https://msdn.microsoft.com/library/windows/hardware/ff537085)

 

 






