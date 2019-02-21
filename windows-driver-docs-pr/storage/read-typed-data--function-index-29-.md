---
title: 读取类型化的数据 （函数索引 29）
description: 此函数读取类型化的块数据区域内的 32 字节块。
ms.assetid: 67B13EBA-F751-4E85-9143-1C331C405B85
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: afad7c003f75a3bd33c4e5c37f4f48e7403c1ebb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520958"
---
# <a name="read-typed-data-function-index-29"></a>读取类型化的数据 （函数索引 29）


此函数读取类型化的块数据区域内的 32 字节块。 此功能，需要使用特定于供应商的寄存器的方案。 它还用于调试。

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
<td align="left"><strong>数据类型</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>数据类型。 这必须是一个中指定的值 *<em>TYPED_BLOCK_DATA</em> （3，0x04）。</p></td>
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
<td align="left"><p>正在读取区域内的块的标识。</p></td>
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
<p>1：数据类型无效。</p>
<p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>数据</strong></td>
<td align="left">32</td>
<td align="left">4</td>
<td align="left"><p>指定的块中的数据。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


平台应使用类型化块数据寄存器来实现此函数。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[写入类型化的数据 （函数索引 30）](write-typed-data--function-index-30-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






