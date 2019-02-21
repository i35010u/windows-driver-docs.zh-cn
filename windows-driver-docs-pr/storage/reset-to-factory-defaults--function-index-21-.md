---
title: 重置为出厂默认值 （函数索引 21）
description: 此函数将返回到供应商预先配置的设置重置 NVDIMM N。
ms.assetid: 64CEF5C8-FC2A-4C6E-829C-27E18A4EDC26
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bb6598830bb7efc03f016b22dfe2949a2904eb42
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540428"
---
# <a name="reset-to-factory-defaults-function-index-21"></a>重置为出厂默认值 （函数索引 21）


此函数将返回到供应商预先配置的设置重置 NVDIMM N。

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
<td align="left"><p>此函数可返回以下特定于函数的错误代码：</p>
<p>1：操作已超时。</p>
<p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关详细信息。</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!请注意\]    &gt;平台应等待三次的最大值保存工厂默认操作完成的超时值 （例如，如果保存超时的最大值为 60 秒，平台应等待 180 秒）。 如果该操作时间超过该时间间隔内，平台应中止操作，并返回特定于函数的错误代码 1 （操作超时）。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






