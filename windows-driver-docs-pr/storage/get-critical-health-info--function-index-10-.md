---
title: 获取关键的运行状况信息（功能索引 10）
description: 此函数返回关键运行状况相关信息。
ms.assetid: 2083628D-FB46-4104-9F70-F7124B35DD04
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aa0417aefa8af1ec41b2f9c27f4bbe938069f176
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355855"
---
# <a name="get-critical-health-info-function-index-10"></a>获取关键的运行状况信息（功能索引 10）


此函数返回关键运行状况相关信息。 调用[获取 NVDIMM N 运行状况信息 (函数索引 11)](get-nvdimm-n-health-info--function-index-11-.md)并[获取能源源运行状况信息 (函数索引 12)](get-energy-source-health-info--function-index-12-.md)以获取进一步与运行状况相关的信息。

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
<td align="left"><strong>严重运行状况信息</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>高级别状态报告的 NVDIMM N 模块的任何问题。</p>
<p>* 字节 0 – <em>MODULE_HEALTH</em> （0，0xA0）</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[获取 NVDIMM N 运行状况信息 （函数索引 11）](get-nvdimm-n-health-info--function-index-11-.md)

[获取能源源运行状况信息 （函数索引 12）](get-energy-source-health-info--function-index-12-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






