---
title: 获取 NVM 阈值（功能索引 5）
description: 此函数返回的生存期百分比警告和错误阈值，如果命中或超过，表示存在问题 NVDIMM n。
ms.assetid: E243AF8B-D70A-4FEF-BB88-ED78C4883D42
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9de60d95aeb322250c93a840d96a3e8ebfd27710
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330048"
---
# <a name="get-nvm-thresholds-function-index-5"></a>获取 NVM 阈值（功能索引 5）


此函数返回的生存期百分比警告和错误阈值，如果命中或超过，表示存在问题 NVDIMM n。

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
<td align="left"><strong>NVM 生存期百分比警告阈值</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>非易失性内存生存期的警告阈值的百分比值。</p>
<p><em>字节 0 – <em>NVM_LIFETIME_WARNING_THRESHOLD</em> （0，0x98）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>NVM 生存期百分比错误阈值</strong></td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left"><p>非易失性内存生存期的错误阈值的百分比值。</p>
<p></em>字节 0 – <em>NVM_LIFETIME_ERROR_THRESHOLD</em> （0，0x90）</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设置 NVM 生存期百分比警告阈值 （函数索引 6）](set-nvm-lifetime-percentage-warning-threshold--function-index-6-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






