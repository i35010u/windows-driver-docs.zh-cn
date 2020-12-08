---
title: 获取操作统计信息（功能索引 13）
description: 此函数返回跟踪 NVDIMM-N 执行的操作的计数器。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 381d1dea51d9fdee1e36ef4494373883f8fc3048
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804577"
---
# <a name="get-operational-statistics-function-index-13"></a>获取操作统计信息（功能索引 13）


此函数返回跟踪 NVDIMM-N 执行的操作的计数器。

> [!NOTE]
> 标记为星形 () 的所有寄存器 \* 都是在可通过字节可寻址的、支持电源的接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>送


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

无。

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>输出


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
<th align="left">字节偏移量</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>请参阅 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a> 获取详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>上次保存操作的持续时间</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>上次保存操作持续时间 (以毫秒或秒为单位) 。</p>
<p><em>Byte 0 – <em>LAST_SAVE_DURATION0</em> (2) </p>
<p></em>字节1– <em>LAST_SAVE_DURATION1</em> (2) </p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>上次还原操作的持续时间</strong></td>
<td align="left">4</td>
<td align="left">8</td>
<td align="left"><p>上次还原操作持续时间 () 以毫秒或秒为单位。</p>
<p><em>Byte 0 – <em>LAST_RESTORE_DURATION0</em> (2) </p>
<p></em>字节1– <em>LAST_RESTORE_DURATION1</em> (2) </p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>上次擦除操作的持续时间</strong></td>
<td align="left">4</td>
<td align="left">12</td>
<td align="left"><p>上次擦除操作的持续时间（以毫秒或秒为单位）。</p>
<p><em>字节0– <em>上次擦除 DURATION_TIME0</em> (2，0x08) </p>
<p></em>字节1– <em>LAST_ERASE DURATION_TIME1</em> (2，0x09) </p>
<p>字节2–保留</p>
<p>字节3–保留</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>已完成的保存操作数</strong></td>
<td align="left">4</td>
<td align="left">16</td>
<td align="left"><p>在 NVDIMM-N 模块的生存期内完成保存操作的次数。</p>
<p><em>Byte 0 – <em>NUM_SAVE_OPS_COUNT0</em> (2) </p>
<p></em>字节1– <em>NUM_SAVE_OPS_COUNT1</em> (2) </p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>已完成的还原操作数</strong></td>
<td align="left">4</td>
<td align="left">20</td>
<td align="left"><p>在 NVDIMM-N 模块的生存期内完成的还原操作的数量。</p>
<p><em>Byte 0 – <em>NUM_RESTORE_OPS_COUNT0 0</em> (2) </p>
<p></em>字节1– <em>NUM_RESTORE_OPS_COUNT1</em> (2) </p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>已完成的擦除操作数</strong></td>
<td align="left">4</td>
<td align="left">24</td>
<td align="left"><p>在 NVDIMM-N 模块的生存期内完成的清除操作的数量。</p>
<p><em>Byte 0 – <em>NUM_ERASE_COUNTS0</em> (2) </p>
<p></em>字节1– <em>NUM_ERASE_COUNTS1</em> (2) </p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>模块的电源周期数量</strong></td>
<td align="left">4</td>
<td align="left">28</td>
<td align="left"><p>在 NVDIMM-N 模块的生存期内的电源循环数。</p>
<p><em>Byte 0 – <em>NUM_MODULE_POWER_CYCLES0</em> (2，0x10) </p>
<p></em>字节1– <em>NUM_MODULE_POWER_CYCLES1</em> (2) </p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






