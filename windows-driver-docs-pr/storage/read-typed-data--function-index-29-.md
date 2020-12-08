---
title: 读取类型化数据（功能索引 29）
description: 此函数读取类型化块数据区域内的32字节块。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2c45a7cde6826593a292788dc293364494dc3c9b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837090"
---
# <a name="read-typed-data-function-index-29"></a>读取类型化数据（功能索引 29）


此函数读取类型化块数据区域内的32字节块。 此功能启用需要使用特定于供应商的寄存器的方案。 它还用于调试。

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
<td align="left"><strong>数据类型</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>数据的类型。 此值必须是 * TYPED_BLOCK_DATA (3<em>TYPED_BLOCK_DATA</em>中指定的值之一) 0x04。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>区域 ID</strong></td>
<td align="left">2</td>
<td align="left">1</td>
<td align="left"><p>正在读取的区域的标识。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>块 ID</strong></td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left"><p>正在区域内读取的块的标识。</p></td>
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
<p>1：数据类型无效。</p>
<p>有关详细信息，请参阅 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a> 。</p></td>
</tr>
<tr class="even">
<td align="left">数据</td>
<td align="left">32</td>
<td align="left">4</td>
<td align="left"><p>指定块中的数据。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


平台应使用类型化块数据寄存器实现此功能。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[写入类型化数据（功能索引 30）](write-typed-data--function-index-30-.md)

[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






