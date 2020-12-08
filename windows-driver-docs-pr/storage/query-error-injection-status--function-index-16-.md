---
title: 查询错误注入状态（功能索引 16）
description: 此函数返回 NVDIMM-N 错误注入的状态。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 123934c7b55ed4e0de0d389ed12c4cb1c36167db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788237"
---
# <a name="query-error-injection-status-function-index-16"></a>查询错误注入状态（功能索引 16）


此函数返回 NVDIMM-N 错误注入的状态。 平台可以选择仅在特定情况下启用错误注入，例如，在用户配置 BIOS 设置之后。

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
<td align="left"><strong>错误注入已启用</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>是否启用错误注入。</p>
<p>如果为0，则禁用错误注入。</p>
<p>如果为1，则启用错误注入。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[注入错误（功能索引 17）](inject-error--function-index-17-.md)

[获取注入的错误（功能索引 18）](get-injected-errors--function-index-18-.md)

[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






