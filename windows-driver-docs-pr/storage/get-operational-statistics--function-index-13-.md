---
title: 获取操作统计信息 （函数索引 13）
description: 此函数将返回跟踪 NVDIMM n。 所执行的操作的计数器
ms.assetid: D396F42E-9B11-46D7-8D9C-FE00B4998DEC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0b10feb825a656d6323e683e802f553d5117d626
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533531"
---
# <a name="get-operational-statistics-function-index-13"></a>获取操作统计信息 （函数索引 13）


此函数将返回跟踪 NVDIMM n。 所执行的操作的计数器

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
<td align="left"><strong>上一次保存操作的持续时间</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>上次保存操作持续时间 （以毫秒或秒）。</p>
<p><em>字节 0 – <em>LAST_SAVE_DURATION0</em> （2，0x04）</p>
<p></em>1 – 字节<em>LAST_SAVE_DURATION1</em> （2，0x05:sp）</p>
<p>保留字节 2 –。</p>
<p>保留字节 3 –。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>最后一个还原操作的持续时间</strong></td>
<td align="left">4</td>
<td align="left">8</td>
<td align="left"><p>最后一个还原操作持续时间 （以毫秒或秒）。</p>
<p><em>字节 0 – <em>LAST_RESTORE_DURATION0</em> （2，0x06:sp）</p>
<p></em>1 – 字节<em>LAST_RESTORE_DURATION1</em> （2，0x07）</p>
<p>保留字节 2 –。</p>
<p>保留字节 3 –。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>最后一次擦除操作的持续时间</strong></td>
<td align="left">4</td>
<td align="left">12</td>
<td align="left"><p>上次清除操作以毫秒或秒的持续时间。</p>
<p><em>字节 0 –<em>最后一个擦除 DURATION_TIME0</em> （2，0x08）</p>
<p></em>1 – 字节<em>LAST_ERASE DURATION_TIME1</em> （2，0x09）</p>
<p>字节 2 – 保留</p>
<p>字节 3 – 保留</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>保存已完成的操作的数量</strong></td>
<td align="left">4</td>
<td align="left">16</td>
<td align="left"><p>已完成保存操作的数通过 NVDIMM N 模块&#39;s 生存期。</p>
<p><em>字节 0 – <em>NUM_SAVE_OPS_COUNT0</em> （2，0x0A）</p>
<p></em>1 – 字节<em>NUM_SAVE_OPS_COUNT1</em> （2，0x0B）</p>
<p>保留字节 2 –。</p>
<p>保留字节 3 –。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>还原已完成的操作数</strong></td>
<td align="left">4</td>
<td align="left">20</td>
<td align="left"><p>通过 NVDIMM N 模块的已完成的还原操作的数目&#39;s 生存期。</p>
<p><em>字节 0 – <em>NUM_RESTORE_OPS_COUNT0 0</em> （2，0x0C）</p>
<p></em>1 – 字节<em>NUM_RESTORE_OPS_COUNT1</em> （2，0x0D）</p>
<p>保留字节 2 –。</p>
<p>保留字节 3 –。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>清除已完成的操作数</strong></td>
<td align="left">4</td>
<td align="left">24</td>
<td align="left"><p>通过 NVDIMM N 模块的已完成的擦除操作的数目&#39;s 生存期。</p>
<p><em>字节 0 – <em>NUM_ERASE_COUNTS0</em> （2，0x0E）</p>
<p></em>1 – 字节<em>NUM_ERASE_COUNTS1</em> （2，0x0F）</p>
<p>保留字节 2 –。</p>
<p>保留字节 3 –。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>模块电源周期数</strong></td>
<td align="left">4</td>
<td align="left">28</td>
<td align="left"><p>通过 NVDIMM N 模块周期 power 数&#39;s 生存期。</p>
<p><em>字节 0 – <em>NUM_MODULE_POWER_CYCLES0</em> （2，0x10）</p>
<p></em>1 – 字节<em>NUM_MODULE_POWER_CYCLES1</em> （2，0x11）</p>
<p>保留字节 2 –。</p>
<p>保留字节 3 –。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






