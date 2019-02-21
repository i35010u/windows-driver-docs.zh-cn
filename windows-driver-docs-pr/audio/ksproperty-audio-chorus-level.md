---
title: KSPROPERTY\_音频\_合唱团\_级别
description: KSPROPERTY\_音频\_合唱团\_级别属性指定合唱团级别。 这是合唱团节点的属性 (KSNODETYPE\_合唱团)。
ms.assetid: 80541b2c-0fb3-4306-8ed2-e524b5a4c113
keywords:
- KSPROPERTY_AUDIO_CHORUS_LEVEL 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_CHORUS_LEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e82e8ea110650f1583f72a2c6fc89c46de7713de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545016"
---
# <a name="kspropertyaudiochoruslevel"></a>KSPROPERTY\_音频\_合唱团\_级别


KSPROPERTY\_音频\_合唱团\_级别属性指定合唱团级别。 这是合唱团节点的属性 ([**KSNODETYPE\_合唱团**](ksnodetype-chorus.md))。

## <span id="ddk_ksproperty_audio_chorus_level_ks"></span><span id="DDK_KSPROPERTY_AUDIO_CHORUS_LEVEL_KS"></span>


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

 

属性值 （操作数据） 是类型为 ULONG，它指定合唱团级别。 合唱团级别值遵循从 0 线性范围为 100\*(65536 的 1/65536) 百分比：

-   值 0x00010000 表示 100%。

-   值 0xFFFFFFFF 表示 100\*(65536 的 1/65536) 百分比。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_合唱团\_级别属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

此属性用于获取和设置合唱团 echo 音量级别。

合唱团是由回显延迟的原始声音和略有调制 echo 的延迟时间创建的语音加倍效果。 有关详细信息，请参阅的说明**IDirectSoundFXChorus** Microsoft Windows SDK 文档中的接口。

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


[**KSNODETYPE\_合唱团**](ksnodetype-chorus.md)

[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

 

 






