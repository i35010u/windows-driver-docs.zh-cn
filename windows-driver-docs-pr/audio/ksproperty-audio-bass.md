---
title: KSPROPERTY\_音频\_低音
description: KSPROPERTY\_音频\_低音属性音节点中指定通道的低音级别 (KSNODETYPE\_音)。
ms.assetid: 64f2f1c9-9275-4fcf-b187-a097b218924e
keywords:
- KSPROPERTY_AUDIO_BASS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_BASS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: babcac2e875afe3331aff6b0e1d6f7001f91f277
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333078"
---
# <a name="kspropertyaudiobass"></a>KSPROPERTY\_音频\_低音


KSPROPERTY\_音频\_低音属性音节点中指定通道的低音级别 ([**KSNODETYPE\_音**](ksnodetype-tone.md))。

## <span id="ddk_ksproperty_audio_bass_ks"></span><span id="DDK_KSPROPERTY_AUDIO_BASS_KS"></span>


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
<td align="left"><p>长</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值属于类型 long 类型的值，指定低音级别。 低音级别值使用以下等级：

是-2147483648-无穷大分贝 （衰减）

在-2147483647 是-32767.99998474 分贝 （衰减） 和

+2147483647 是 +32767.99998474 分贝 （提升）。

由整数值介于-2147483648 到 +2147483647，表示分贝范围位置

此范围具有的分辨率为 1/65536 分贝。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_低音属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

筛选器将会成功 KSPROPERTY\_音频\_指定一个值，不在筛选器的范围，但将固定到支持的范围值的低音设置属性请求。 在后续请求中获取此属性，但是，它将输出所用的实际值。

音节点的级别、 中间频率级别、 低音级别和低音增强高音控制可以支持属性。 有关详细信息，请参阅[ **KSNODETYPE\_音**](ksnodetype-tone.md)。

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

[**KSNODETYPE\_音**](ksnodetype-tone.md)

 

 






