---
title: 获取能量源运行状况信息（功能索引 12）
description: 此函数返回有关 (ES) 模块的能源源运行状况的信息。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 094ee792c9d9b9f093ce4de5041b837046f305e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835291"
---
# <a name="get-energy-source-health-info-function-index-12"></a>获取能量源运行状况信息（功能索引 12）


此函数返回有关 (ES) 模块的能源源运行状况的信息。 如果 ES 是托管主机并且运行状况信息不可用，则此函数可能返回失败状态。

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
<td align="left"><p>此函数可能返回以下 Function-Specific 错误代码：</p>
<p>1：平台不支持 ES 运行状况信息。</p>
<p>有关详细信息，请参阅 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 生存期百分比</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>最后一个已知的 ES 生存期百分比。</p>
<p><em>Byte 0 – <em>ES_LIFETIME</em> (1) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 当前温度</strong></td>
<td align="left">2</td>
<td align="left">5</td>
<td align="left"><p>ES 温度（摄氏度）。 最小值为 0。</p>
<p></em>Byte 0 – <em>ES_TEMP0</em> (1) </p>
<p><em>字节1– <em>ES_TEMP1</em> (1) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>总运行时间</strong></td>
<td align="left">4</td>
<td align="left">7</td>
<td align="left"><p>自制造后) ES 运行的时间 (小时。</p>
<p></em>Byte 0 – <em>ES_RUNTIME0</em> (1) </p>
<p>* Byte 1 – <em>ES_RUNTIME1</em> (1) </p>
<p>字节2–保留</p>
<p>字节3–保留</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[获取 NVDIMM-N 运行状况信息（功能索引 11）](get-nvdimm-n-health-info--function-index-11-.md)

[获取能量源运行状况信息（功能索引 12）](get-energy-source-health-info--function-index-12-.md)

[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






