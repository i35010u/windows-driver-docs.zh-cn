---
title: 获取注入的错误（功能索引 18）
description: 此函数返回有关当前注入错误的信息。
ms.assetid: 60D4E64C-ABB6-4B24-971F-594306D8C07C
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bcf77d0d8e67a87e4d60189fd9de968f8cd65ff5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379759"
---
# <a name="get-injected-errors-function-index-18"></a>获取注入的错误（功能索引 18）


此函数返回有关当前注入错误的信息。

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
<td align="left"><strong>插入操作失败</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>哪些操作或非易失性内存当前注入错误的信息。</p>
<p><em>字节 0 – <em>INJECT_OPS_FAILURES</em> （2，0x60）</p>
<p></em>字节 1 – 如果<em>INJECT_BAD_BLOCKS</em>为"1"（7 位的字节 0），这是<em> <em>INJECT_BAD_BLOCK_CAP</em> （2，0x67）。 否则，这应为 0。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>能量源故障注入</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>有关哪些能源源 (ES) 当前注入错误的信息。</p>
<p></em>字节 0 – <em>INJECT_ES_FAILURES</em> （2，0x64）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>注入的固件更新失败</strong></td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left"><p>有关哪种固件目前注入操作错误的信息。</p>
<p>* 字节 0 – <em>INJECT_FW_FAILURES</em> （2、 0x65）</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


如果禁用了平台错误注入，此函数应成功并返回相同的信息，如果有当前注入任何错误。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[注入错误 （函数索引 17）](inject-error--function-index-17-.md)

[查询错误注入状态 （函数索引 16）](query-error-injection-status--function-index-16-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






