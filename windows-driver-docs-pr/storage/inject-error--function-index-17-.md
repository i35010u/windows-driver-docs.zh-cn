---
title: 注入错误 （函数索引 17）
description: 此函数会注入 NVDIMM N 模块固件中的错误。 此函数的用途是启用软件验证。
ms.assetid: 4D77DC95-25BC-4D28-83B7-7A62383803E6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 25d749b13a6a4b3e34629532c942e0d391af03f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534888"
---
# <a name="inject-error-function-index-17"></a>注入错误 （函数索引 17）


此函数会注入 NVDIMM N 模块固件中的错误。 此函数的用途是启用软件验证。 该平台可以选择仅启用在特定情况下，错误注入，例如用户配置的 BIOS 设置后。 宿主可能调用[查询错误注入状态 (函数索引 16)](query-error-injection-status--function-index-16-.md)若要了解是否错误注入启用的函数。

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
<td align="left"><strong>插入操作故障</strong></td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left"><p>指定将注入哪些操作或非易失性内存错误。</p>
<p><em>字节 0 – <em>INJECT_OPS_FAILURES</em> （2，0x60）</p>
<p></em>字节 1 – 如果<em>INJECT_BAD_BLOCKS</em>为 1 （7 位的字节 0），这是<em>INJECT_BAD_BLOCK_CAP</em> （2，0x67）。 否则，它应为 0。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>插入能源源故障</strong></td>
<td align="left">1</td>
<td align="left">2</td>
<td align="left"><p>指定将注入哪些能源源 (ES) 错误。</p>
<p><em>字节 0 – <em>INJECT_ES_FAILURES</em> （2，0x64）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>注入固件更新失败</strong></td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left"><p>指定将注入的固件操作错误。</p>
<p></em>字节 0 – <em>INJECT_FW_FAILURES</em> （2、 0x65）</p></td>
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
<p>1：错误注入处于禁用状态。</p>
<p>2：无法注入一个或多个错误，因为它们不受支持。</p>
<p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关详细信息。</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!请注意\]    &gt;返回特定于函数的错误代码 2 时，剩余注入已成功插入的将任何错误。 如果此函数返回特定于函数的错误代码 2，则调用[获取注入错误 (函数索引 18)](get-injected-errors--function-index-18-.md)检索可以注入哪些错误。

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


某些错误注入功能是可选的可能不支持的设备。 请参阅相应字节可寻址能源支持接口 JEDEC 列表可选错误注入的规范。

在平台必须检测到主机尝试将不受支持的错误。 它通过写入到错误注入注册，然后读取同一个寄存器并验证所有预期的位设置实现的。 例如，在平台执行以下操作以插入操作失败：

1.  将字节 0 的值写入**注入操作故障**字段*插入\_OPS\_故障*注册。

2.  读取*插入\_OPS\_故障*注册。

3.  如果新的值*插入\_OPS\_故障*匹配的 0 字节**注入操作失败**字段中，返回成功消息。 否则，返回特定于函数的错误代码 2。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[查询错误注入状态 （函数索引 16）](query-error-injection-status--function-index-16-.md)

[获取注入错误 （函数索引 18）](get-injected-errors--function-index-18-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






