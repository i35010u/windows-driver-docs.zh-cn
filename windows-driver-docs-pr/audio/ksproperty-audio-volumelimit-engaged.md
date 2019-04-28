---
title: KSPROPERTY\_音频\_VOLUMELIMIT\_ENGAGED
description: KSPROPERTY\_音频\_VOLUMELIMIT\_卡入到位，是一个新的 KS 属性，已添加到 KSPROPSETID\_音频在 Windows 8.1 中设置的属性。
ms.assetid: 0DAC584A-EC17-4280-B90D-2D9DDB620479
keywords:
- KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_VOLUMELIMIT_ENGAGED
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b4c5432521ee9343723805b5ab5ced22ed5c518
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332889"
---
# <a name="kspropertyaudiovolumelimitengaged"></a>KSPROPERTY\_音频\_VOLUMELIMIT\_ENGAGED


KSPROPERTY\_音频\_VOLUMELIMIT\_卡入到位，是一个新的 KS 属性，已添加到 KSPROPSETID\_音频在 Windows 8.1 中设置的属性。

KSPROPERTY\_音频\_VOLUMELIMIT\_ENGAGED 属性请求将传递到基础驱动程序的最终用户的卷级别的限制首选项。 此属性的作用域是每个 pin （或每个音频终结点，从最终用户的角度来看）。

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
<td align="left"><p>Pin 实例</p></td>
<td align="left"><p>KSP_PIN</p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值为类型 BOOL，并指示最终用户是否允许要超过一定范围的最大卷。 值为 TRUE 指示最终用户具有允许音量级别要对已发布的限制，而 FALSE 表示相反的情况。 在子帐户的情况下的值将始终为 FALSE。

驱动程序将此属性的值存储在一个内部变量，并在启动期间初始化的值为 TRUE。 虽然此属性为 TRUE，该驱动程序限制的最大音量级别。 该属性设置为 FALSE 时，驱动程序可以删除这些限制。

该驱动程序还可以自动更改此属性的值。 例如，驱动程序可以自动切换为 FALSE，true，则从属性值，然后开始后已过一段特定的声音级别以上的时间内限制音量级别。

只要属性值发生更改，而不考虑它是自动还是由于调用方设置的属性值，则驱动程序应生成 KSEVENT\_PINCAPS\_VOLUMELIMITCHANGE 事件。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_VOLUMELIMIT\_ENGAGED 属性请求将返回状态\_成功时请求已成功提交。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

 

 





