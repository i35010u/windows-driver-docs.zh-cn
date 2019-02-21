---
title: 查询错误注入状态 （函数索引 16）
description: 此函数返回 NVDIMM N 错误注入的状态。
ms.assetid: 7CE07551-666F-4E07-8115-806F6256B595
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1f12342d3466f019ff23a431496bb4c4f86b77af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519228"
---
# <a name="query-error-injection-status-function-index-16"></a>查询错误注入状态 （函数索引 16）


此函数返回 NVDIMM N 错误注入的状态。 该平台可以选择仅启用在特定情况下，错误注入，例如用户配置的 BIOS 设置后。

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
<td align="left"><strong>启用的错误注入</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>该值指示是否启用错误注入。</p>
<p>如果为 0，已禁用错误注入。</p>
<p>如果为 1，启用错误注入。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[注入错误 （函数索引 17）](inject-error--function-index-17-.md)

[获取注入错误 （函数索引 18）](get-injected-errors--function-index-18-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






