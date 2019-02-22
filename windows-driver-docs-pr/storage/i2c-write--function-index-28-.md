---
title: I2C 写入 （函数索引 28）
description: 此函数将写入 Inter-Integrated 线路 (I2C) 注册。
ms.assetid: 72DE8C76-B910-4979-BCEC-7CFFABA4CC19
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: edd5f2dea1c80235154e4042a7fc2f70aee8e67f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522729"
---
# <a name="i2c-write-function-index-28"></a>I2C 写入 （函数索引 28）


此函数将写入 Inter-Integrated 线路 (I2C) 注册。 此功能，需要使用特定于供应商的寄存器的方案。 它还用于调试。

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
<td align="left"><strong>页面</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>I2C 注册所在的页。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Offset</strong></td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left"><p>注册的页面内偏移量。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>数据</strong></td>
<td align="left">1</td>
<td align="left">2</td>
<td align="left"><p>要写入到注册的数据。</p></td>
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
<p>1：无效的页面。</p>
<p>2：无法写入此寄存器。</p>
<p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关详细信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[I2C 读取 （函数索引 27）](i2c-read--function-index-27-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






