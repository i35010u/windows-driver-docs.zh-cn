---
title: 获取能量源运行状况信息（功能索引 12）
description: 此函数返回能源源 (ES) 模块的运行状况的信息。
ms.assetid: A2044F2A-79DA-4D3A-93B7-BE9D389DA399
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a5458376ec4e849e6d95b795b7fab113dc66d8d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355839"
---
# <a name="get-energy-source-health-info-function-index-12"></a>获取能量源运行状况信息（功能索引 12）


此函数返回能源源 (ES) 模块的运行状况的信息。 如果 ES 是主机托管和运行状况信息不可用，则此函数可返回的故障状态。

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
<td align="left"><p>此函数可返回以下特定于函数的错误代码：</p>
<p>1：平台不支持 ES 运行状况信息。</p>
<p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>ES 生存期百分比</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>最后一个已知的 ES 生存期百分比。</p>
<p><em>字节 0 – <em>ES_LIFETIME</em> （1，0x70）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ES 当前温度</strong></td>
<td align="left">2</td>
<td align="left">5</td>
<td align="left"><p>ES 温度以摄氏度。 最小值为 0。</p>
<p></em>字节 0 – <em>ES_TEMP0</em> （1，0x71）</p>
<p><em>1 – 字节<em>ES_TEMP1</em> （1，0x72）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>总运行时</strong></td>
<td align="left">4</td>
<td align="left">7</td>
<td align="left"><p>时间 （以小时为单位） ES 已被操作，因为它制造。</p>
<p></em>字节 0 – <em>ES_RUNTIME0</em> （1，0x73）</p>
<p>* 字节 1 – <em>ES_RUNTIME1</em> （1，0x74）</p>
<p>字节 2 – 保留</p>
<p>字节 3 – 保留</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[获取 NVDIMM N 运行状况信息 （函数索引 11）](get-nvdimm-n-health-info--function-index-11-.md)

[获取能源源运行状况信息 （函数索引 12）](get-energy-source-health-info--function-index-12-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






