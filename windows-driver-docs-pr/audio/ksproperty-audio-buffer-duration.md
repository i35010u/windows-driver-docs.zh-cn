---
title: KSPROPERTY\_音频\_缓冲区\_持续时间
description: KSPROPERTY\_音频\_缓冲区\_持续时间属性，可用于报告的持续时间为客户端应用程序缓冲区的大小。
ms.assetid: 9749464f-d351-468b-b785-fa84705ef2c0
keywords:
- KSPROPERTY_AUDIO_BUFFER_DURATION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_BUFFER_DURATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 749bbdc6239b9b986303523494aea91bc1568eec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566363"
---
# <a name="kspropertyaudiobufferduration"></a>KSPROPERTY\_音频\_缓冲区\_持续时间


KSPROPERTY\_音频\_缓冲区\_持续时间属性，可用于报告的持续时间为客户端应用程序缓冲区的大小。

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
<td align="left"><p>Pin</p></td>
<td align="left"><p>KSPROPERTY</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值是类型为 ULONG，表示以毫秒为单位的客户端缓冲区持续时间。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_缓冲区\_持续时间属性请求将返回状态\_成功以指示属性请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

您可以调整同步的音频数据捕获，以帮助提高您的 USB 音频设备的性能的请求的持续的时间。 较短的持续时间减少了延迟，但它也意味着 USB 音频堆栈必须进行更频繁地延缓的过程调用 (DPC)，这可能会导致性能下降。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

 

 





