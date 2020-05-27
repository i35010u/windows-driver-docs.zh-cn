---
title: 获取供应商日志页大小（功能索引 14）
description: 此函数返回供应商日志页的大小，以便主机了解它需要分配以读取供应商日志页的缓冲区大小。
ms.assetid: 24211D67-1D36-4711-B87B-C99546E206FC
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aafc1d581b67a9f36a8e72db53827f755297dcab
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851700"
---
# <a name="get-vendor-log-page-size-function-index-14"></a>获取供应商日志页大小（功能索引 14）


此函数返回供应商日志页的大小，以便主机了解它需要分配以读取供应商日志页的缓冲区大小。

> [!NOTE]
> 标有星号（）的所有寄存器 \* 都是在可通过字节寻址的可处理电源接口规范中定义的寄存器。

 

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>请参阅<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>获取详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>供应商日志页面大小</strong></td>
<td align="left">4</td>
<td align="left">4</td>
<td align="left"><p>供应商日志页的大小为32个字节的倍数。</p>
<p>* Byte 0 – <em>VENDOR_LOG_PAGE_SIZE</em> （0，0x31）</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[获取供应商日志页（功能索引 15）](get-vendor-log-page--function-index-15-.md)

[\_用于字节寻址的支持能源的函数类的 DSM 接口（Function Interface 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






