---
title: 读取类型化数据（功能索引 29）
description: 此函数读取类型化块数据区域内的32字节块。
ms.assetid: 67B13EBA-F751-4E85-9143-1C331C405B85
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6ba8efde81dbd14bf19c6c28cb367385916cb2e9
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851314"
---
# <a name="read-typed-data-function-index-29"></a>读取类型化数据（功能索引 29）


此函数读取类型化块数据区域内的32字节块。 此功能启用需要使用特定于供应商的寄存器的方案。 它还用于调试。

> [!NOTE]
> 标有星号（）的所有寄存器 \* 都是在可通过字节寻址的可处理电源接口规范中定义的寄存器。

 

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>数据类型</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>数据的类型。 这必须是在 *<em>TYPED_BLOCK_DATA</em> （3，0x04）中指定的值之一。</p></td>
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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>此函数可以返回以下特定于函数的错误代码：</p>
<p>1：数据类型无效。</p>
<p>有关详细信息，请参阅<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>数据</strong></td>
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

[\_用于字节寻址的支持能源的函数类的 DSM 接口（Function Interface 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






