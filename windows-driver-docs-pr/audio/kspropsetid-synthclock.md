---
title: KSPROPSETID\_SynthClock
description: KSPROPSETID\_SynthClock
ms.assetid: 8baad0d2-ea86-4d27-8fb0-03cdd9e978f0
keywords:
- KSPROPSETID_SynthClock
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4fc138212d48982333cced8466b1794e6e3e800
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332471"
---
# <a name="kspropsetidsynthclock"></a>KSPROPSETID\_SynthClock


## <span id="ddk_kspropsetid_synthclock_ks"></span><span id="DDK_KSPROPSETID_SYNTHCLOCK_KS"></span>


`KSPROPSETID_SynthClock`属性集用于获取 DirectMusic 合成器的主时钟时间。 此集包含单个 DirectMusic 筛选器对象的属性。 Dmu 端口驱动程序实现此属性的处理程序。

有关详细信息，请参阅[Master 时钟](https://msdn.microsoft.com/library/windows/hardware/ff567717)并[合成器计时](https://msdn.microsoft.com/library/windows/hardware/ff538449)。

在此集中的属性项由 KSPROPERTY\_SYNTHCLOCK 枚举值，如标头中定义文件 Dmusprop.h。

## <span id="ddk_ksproperty_synth_masterclock_ks"></span><span id="DDK_KSPROPERTY_SYNTH_MASTERCLOCK_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

KSPROPERTY\_合成器\_MASTERCLOCK 属性用于获取主时钟时间。

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
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>ULONGLONG</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值属于类型 ULONGLONG，表示主时钟时间。 以 100 毫微秒为单位指定此时间。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_合成\_MASTERCLOCK 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

有关详细信息，请参阅[Master 时钟](https://msdn.microsoft.com/library/windows/hardware/ff567717)。

 

 





