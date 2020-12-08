---
title: 注入错误（功能索引 17）
description: 此函数在 NVDIMM-N 模块固件中注入错误。 此函数的目的是启用软件验证。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 16ee6495c91e60b72a964635b4403b098b049b8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811699"
---
# <a name="inject-error-function-index-17"></a>注入错误（功能索引 17）


此函数在 NVDIMM-N 模块固件中注入错误。 此函数的目的是启用软件验证。 平台可以选择仅在特定情况下启用错误注入，例如，在用户配置 BIOS 设置之后。 宿主可以调用 [ (函数索引 16) 的查询错误注入状态 ](query-error-injection-status--function-index-16-.md) ，以了解是否已启用错误注入函数。

> [!NOTE]
> 标记为星形 () 的所有寄存器 \* 都是在可通过字节可寻址的、支持电源的接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>送


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
<th align="left">字节偏移量</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>注入操作失败</strong></td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left"><p>指定将注入哪个操作或非易失性的内存错误。</p>
<p><em>Byte 0 – <em>INJECT_OPS_FAILURES</em> (2) </p>
<p></em>字节1–如果 <em>INJECT_BAD_BLOCKS</em> 为 1 (第7位，第7字节) ，则 <em>INJECT_BAD_BLOCK_CAP</em> () 。 否则，它应为0。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>注入能量源故障</strong></td>
<td align="left">1</td>
<td align="left">2</td>
<td align="left"><p>指定将注入 (ES) 错误的能源来源。</p>
<p><em>Byte 0 – <em>INJECT_ES_FAILURES</em> (2) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>插入固件更新失败</strong></td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left"><p>指定将注入哪些固件操作错误。</p>
<p></em>Byte 0 – <em>INJECT_FW_FAILURES</em> (2) </p></td>
</tr>
</tbody>
</table>

 

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
<td align="left"><p>此函数可能返回以下 Function-Specific 错误代码：</p>
<p>1：错误注入处于禁用状态。</p>
<p>2：未能注入一个或多个错误，因为它们不受支持。</p>
<p>有关详细信息，请参阅 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a> 。</p></td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> 返回 Function-Specific 错误代码2时，成功注入的任何错误都将保持注入。 如果此函数返回 Function-Specific 错误代码2，请调用 [ (函数索引 18) 中注入错误 ](get-injected-errors--function-index-18-.md) ，以检索无法插入的错误。

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


某些错误注入功能是可选的，可能不受设备支持。 有关可选错误注入的列表，请参阅相应的字节可寻址电源支持的接口 JEDEC 规范。

平台必须检测主机是否试图注入不受支持的错误。 它通过向错误注入注册并读取同一寄存器来完成此工作，& 验证是否设置了所有的目标位。 例如，平台执行以下操作来注入操作故障：

1.  将 **插入操作失败** 字段的字节0的值写入 *插入操作 \_ \_ 失败* 的注册。

2.  读取 *插入 \_ OPS \_ 故障* 注册。

3.  如果 *注入操作 \_ \_ 失败* 的新值与 **插入操作失败** 字段的字节0匹配，则返回 success。 否则，返回 Function-Specific 错误代码2。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[查询错误注入状态（功能索引 16）](query-error-injection-status--function-index-16-.md)

[获取注入的错误（功能索引 18）](get-injected-errors--function-index-18-.md)

[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






