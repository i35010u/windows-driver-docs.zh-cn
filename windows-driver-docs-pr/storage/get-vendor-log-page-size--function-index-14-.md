---
title: 获取供应商日志页大小 （函数索引 14）
description: 此函数返回的供应商大小日志页，以便让主机知道它需要分配读取日志页的供应商的缓冲区的大小。
ms.assetid: 24211D67-1D36-4711-B87B-C99546E206FC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 772c34ded9f25f64eea11d6a06e0f626b02ff557
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542980"
---
# <a name="get-vendor-log-page-size-function-index-14"></a>获取供应商日志页大小 （函数索引 14）


此函数返回的供应商大小日志页，以便让主机知道它需要分配读取日志页的供应商的缓冲区的大小。

&gt; \[!请注意\]    &gt;用一个星号标记所有寄存器 (\*) 字节可寻址能源支持接口规范中定义的寄存器。

 

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
<td align="left"><p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>供应商日志页面大小</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>供应商日志页中的 32 字节的序列图的大小。</p>
<p>*Byte 0 – <em>VENDOR_LOG_PAGE_SIZE</em> (0, 0x31)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[获取供应商日志页 （函数索引 15）](get-vendor-log-page--function-index-15-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






