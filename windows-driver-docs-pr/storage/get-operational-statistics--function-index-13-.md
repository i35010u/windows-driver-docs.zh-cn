---
title: 获取操作统计信息（功能索引 13）
description: 此函数返回跟踪 NVDIMM-N 执行的操作的计数器。
ms.assetid: D396F42E-9B11-46D7-8D9C-FE00B4998DEC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 46d7975d85c7620b758ad2e83f3dc5411b6718d7
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851448"
---
# <a name="get-operational-statistics-function-index-13"></a>获取操作统计信息（功能索引 13）


此函数返回跟踪 NVDIMM-N 执行的操作的计数器。

> [!NOTE]
> 标有星号（）的所有寄存器 \* 都是在可通过字节寻址的可处理电源接口规范中定义的寄存器。

 

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>请参阅<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>获取详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>上次保存操作的持续时间</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>上次保存操作的持续时间（以毫秒或秒为单位）。</p>
<p><em>Byte 0 – <em>LAST_SAVE_DURATION0</em> （2，0x04）</p>
<p></em>Byte 1 – <em>LAST_SAVE_DURATION1</em> （2，0x05）</p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>上次还原操作的持续时间</strong></td>
<td align="left">4</td>
<td align="left">8</td>
<td align="left"><p>上次还原操作持续时间（以毫秒或秒为单位）。</p>
<p><em>Byte 0 – <em>LAST_RESTORE_DURATION0</em> （2，0x06）</p>
<p></em>Byte 1 – <em>LAST_RESTORE_DURATION1</em> （2，0x07）</p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>上次擦除操作的持续时间</strong></td>
<td align="left">4</td>
<td align="left">12</td>
<td align="left"><p>上次擦除操作的持续时间（以毫秒或秒为单位）。</p>
<p><em>字节0–<em>上次擦除 DURATION_TIME0</em> （2，0x08）</p>
<p></em>字节1– <em>LAST_ERASE DURATION_TIME1</em> （2，0x09）</p>
<p>字节2–保留</p>
<p>字节3–保留</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>已完成的保存操作数</strong></td>
<td align="left">4</td>
<td align="left">16</td>
<td align="left"><p>在 NVDIMM-N 模块的生存期内完成保存操作的次数。</p>
<p><em>Byte 0 – <em>NUM_SAVE_OPS_COUNT0</em> （2，0x0A）</p>
<p></em>Byte 1 – <em>NUM_SAVE_OPS_COUNT1</em> （2，0x0B）</p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>已完成的还原操作数</strong></td>
<td align="left">4</td>
<td align="left">20</td>
<td align="left"><p>在 NVDIMM-N 模块的生存期内完成的还原操作的数量。</p>
<p><em>Byte 0 – <em>NUM_RESTORE_OPS_COUNT0 0</em> （2，0x0C）</p>
<p></em>Byte 1 – <em>NUM_RESTORE_OPS_COUNT1</em> （2，0x0D）</p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>已完成的擦除操作数</strong></td>
<td align="left">4</td>
<td align="left">24</td>
<td align="left"><p>在 NVDIMM-N 模块的生存期内完成的清除操作的数量。</p>
<p><em>Byte 0 – <em>NUM_ERASE_COUNTS0</em> （2，0x0E）</p>
<p></em>Byte 1 – <em>NUM_ERASE_COUNTS1</em> （2，0x0F）</p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>模块的电源周期数量</strong></td>
<td align="left">4</td>
<td align="left">28</td>
<td align="left"><p>在 NVDIMM-N 模块的生存期内的电源循环数。</p>
<p><em>Byte 0 – <em>NUM_MODULE_POWER_CYCLES0</em> （2，0x10）</p>
<p></em>Byte 1 – <em>NUM_MODULE_POWER_CYCLES1</em> （2，0x11）</p>
<p>Byte 2 – Reserved。</p>
<p>字节3–预留。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[\_用于字节寻址的支持能源的函数类的 DSM 接口（Function Interface 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






