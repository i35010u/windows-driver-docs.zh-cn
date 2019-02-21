---
title: 获取能源源阈值 （函数索引 7）
description: 此函数返回的如果命中或超过，表示与能源源 (ES) 有问题的警告和错误阈值。
ms.assetid: 12B7D7CF-DB65-42A5-9831-F0D85BED2574
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f2dad016b5e1db55de9e96a17dbcc697ab70e1b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526536"
---
# <a name="get-energy-source-thresholds-function-index-7"></a>获取能源源阈值 （函数索引 7）


此函数返回的如果命中或超过，表示与能源源 (ES) 有问题的警告和错误阈值。 如果 ES 是主机托管和平台不支持的阈值，此函数可返回的故障状态。

&gt; \[!请注意\]    &gt;用一个星号标记所有寄存器 (\*) 字节可寻址能源支持接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>输入


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

无。

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>Output


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">字节长度</th>
<th align="left">字节偏移</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 生存期百分比警告阈值</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>ES 生存期的警告阈值的百分比值。</p>
<p><em>字节 0 – <em>ES_LIFETIME_WARNING_THRESHOLD</em> （0，0x99）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 生存期百分比错误阈值</strong></td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left"><p>ES 生存期的错误阈值的百分比值。</p>
<p></em>字节 0 – <em>ES_LIFETIME_ERROR_THRESHOLD</em> （0，0x91）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 温度警告阈值</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>ES 温度的警告阈值的百分比值。</p>
<p><em>字节 0 – <em>ES_TEMP_WARNING_THRESHOLD</em> （0，0x9A）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 温度错误阈值</strong></td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left"><p>ES 温度的错误阈值的百分比值。</p>
<p></em>字节 0 – <em>ES_TEMP_ERROR_THRESHOLD</em> （0，0x92）</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[设置能量源生存期警告阈值 （函数索引 8）](set-energy-source-lifetime-warning-threshold--function-index-8-.md)

[设置能源源温度警告阈值 （函数索引 9）](set-energy-source-temperature-warning-threshold--function-index-9-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






