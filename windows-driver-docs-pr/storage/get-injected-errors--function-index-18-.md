---
title: 获取注入的错误（功能索引 18）
description: 此函数返回有关当前注入的错误的信息。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8592d621ef0f7c59f1a2bf8cba84d489eede74ab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835289"
---
# <a name="get-injected-errors-function-index-18"></a>获取注入的错误（功能索引 18）


此函数返回有关当前注入的错误的信息。

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
<td align="left"><p>请参阅 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a> 获取详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>注入的操作失败</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>当前注入了哪些操作或非易失性内存错误的相关信息。</p>
<p><em>Byte 0 – <em>INJECT_OPS_FAILURES</em> (2) </p>
<p></em>字节1–如果<em>INJECT_BAD_BLOCKS</em>为 "1" (字节 0) 第7位，则 <em> <em>INJECT_BAD_BLOCK_CAP</em> (2，0x67) 。 否则，此应为0。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>插入的能量源故障</strong></td>
<td align="left">1</td>
<td align="left">6</td>
<td align="left"><p>有关当前注入哪个能量源 (ES) 错误的信息。</p>
<p></em>Byte 0 – <em>INJECT_ES_FAILURES</em> (2) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>插入固件更新失败</strong></td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left"><p>当前插入了哪些固件操作错误的相关信息。</p>
<p>* Byte 0 – <em>INJECT_FW_FAILURES</em> (2) </p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


如果平台禁用了错误注入，此函数应成功并返回相同的信息，就好像当前没有插入任何错误一样。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[注入错误（功能索引 17）](inject-error--function-index-17-.md)

[查询错误注入状态（功能索引 16）](query-error-injection-status--function-index-16-.md)

[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






