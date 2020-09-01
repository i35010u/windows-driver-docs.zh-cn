---
title: KSPROPSETID \_ SynthClock
description: KSPROPSETID \_ SynthClock
ms.assetid: 8baad0d2-ea86-4d27-8fb0-03cdd9e978f0
keywords:
- KSPROPSETID_SynthClock
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c11c1cd3f2bdfdb9f5f21c0fc4597b040c99eb45
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211455"
---
# <a name="kspropsetid_synthclock"></a>KSPROPSETID \_ SynthClock


## <span id="ddk_kspropsetid_synthclock_ks"></span><span id="DDK_KSPROPSETID_SYNTHCLOCK_KS"></span>


`KSPROPSETID_SynthClock`属性集用于获取 DirectMusic 合成器的主时钟时间。 此集包含 DirectMusic 筛选器对象的单个属性。 Dmu 端口驱动程序实现此属性的处理程序。

有关详细信息，请参阅 [主时钟](../stream/master-clocks.md) 和 [合成器计时](./synthesizer-timing.md)。

此集中的属性项由 KSPROPERTY \_ SYNTHCLOCK 枚举值指定，如标头文件 Dmusprop 中所定义。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

KSPROPERTY \_ 合成 \_ MASTERCLOCK 属性用于获取主时钟时间。

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
<th align="left">获取</th>
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
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>ULONGLONG</p></td>
</tr>
</tbody>
</table>

 

操作数据) 的属性值 (类型为 ULONGLONG 并表示主时钟时间。 此时间以100毫微秒为单位指定。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 合成 \_ MASTERCLOCK 属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

有关详细信息，请参阅 [主时钟](../stream/master-clocks.md)。

 

