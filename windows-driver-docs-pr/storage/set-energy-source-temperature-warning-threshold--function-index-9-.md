---
title: 设置能量源温度警告阈值（功能索引 9）
description: 此函数将运行能量源 (ES) 温度的警告阈值。
ms.assetid: AE624191-87F2-4673-A31B-CABE94623535
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8cd26d9b84f1d9e3a57b5f0a21c5e7845997cb91
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376427"
---
# <a name="set-energy-source-temperature-warning-threshold-function-index-9"></a>设置能量源温度警告阈值（功能索引 9）


此函数将运行能量源 (ES) 温度的警告阈值。 如果 ES 是主机托管和阈值在平台上不支持此函数可返回的故障状态。

&gt; \[!请注意\]    &gt;用一个星号标记所有寄存器 (\*) 字节可寻址能源支持接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>输入


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

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
<td align="left"><strong>ES 生存期温度警告阈值</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>警告阈值的新值 （单位为摄氏度）。</p>
<p>平台应写入此值设置为 *<em>ES_TEMP_WARNING_THRESHOLD</em> （0，0x99） 注册。</p></td>
</tr>
</tbody>
</table>

 

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
<p>1：平台不支持 ES 阈值。</p>
<p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关详细信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设置能量源生存期警告阈值 （函数索引 8）](set-energy-source-lifetime-warning-threshold--function-index-8-.md)

[获取能源源阈值 （函数索引 7）](get-energy-source-thresholds--function-index-7-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






