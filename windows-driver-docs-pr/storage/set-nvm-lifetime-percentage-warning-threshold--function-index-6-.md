---
title: 设置 NVM 生存期百分比警告阈值 （函数索引 6）
description: 此函数将剩余的非易失性内存生存期百分比的警告阈值。
ms.assetid: B5568876-D9E1-4086-8819-FC5FF6BC2C15
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: af49417ca18f17f9e56f710921d7df32a848ebc2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543549"
---
# <a name="set-nvm-lifetime-percentage-warning-threshold-function-index-6"></a>设置 NVM 生存期百分比警告阈值 （函数索引 6）


此函数将剩余的非易失性内存生存期百分比的警告阈值。

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
<td align="left"><strong>NVM 生存期百分比警告阈值</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>警告阈值必须介于 0 和 100 之间的百分比值。</p>
<p>平台应写入此值设置为 *<em>NVM_LIFETIME_WARNING_THRESHOLD （0，0x98）</em>注册。</p></td>
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
<td align="left"><p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[获取 NVM 阈值 （函数索引 5）](get-nvm-thresholds--function-index-5-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






