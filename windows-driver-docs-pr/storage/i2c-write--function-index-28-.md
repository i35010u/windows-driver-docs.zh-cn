---
title: I2C 写入（功能索引 28）
description: 此函数 (I2C) register 写入 Inter-Integrated 电路。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9bc096dde97c434ab9be5eb5a2b47819e5314d99
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804467"
---
# <a name="i2c-write-function-index-28"></a>I2C 写入（功能索引 28）


此函数 (I2C) register 写入 Inter-Integrated 电路。 此功能启用需要使用特定于供应商的寄存器的方案。 它还用于调试。

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
<td align="left"><strong>页</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>I2C 寄存器所在的页面。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Offset</strong></td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left"><p>寄存器在页面内的偏移量。</p></td>
</tr>
<tr class="odd">
<td align="left">数据</td>
<td align="left">1</td>
<td align="left">2</td>
<td align="left"><p>要写入注册的数据。</p></td>
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
<p>1：页无效。</p>
<p>2：无法将此寄存器写入。</p>
<p>有关详细信息，请参阅 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a> 。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[I2C 读取（功能索引 27）](i2c-read--function-index-27-.md)

[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






