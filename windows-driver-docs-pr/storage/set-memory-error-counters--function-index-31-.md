---
title: 设置内存错误计数器（功能索引 31）
description: 此函数将跟踪可纠正的和不可纠正的内存错误事件的计数器设置为调用方指定的值。 此函数的目的是启用软件验证。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6050fcb697ace0a50900d5fc2d6b391a7e8f1462
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782121"
---
# <a name="set-memory-error-counters-function-index-31"></a>设置内存错误计数器（功能索引 31）


此函数将跟踪可纠正的和不可纠正的内存错误事件的计数器设置为调用方指定的值。 此函数的目的是启用软件验证。

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
<td align="left"><strong>DRAM 无法纠正的 ECC 错误计数</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>平台从 NVDIMM-N 模块检测到的无法纠正的 ECC 错误数。</p>
<p>平台应将此值写入 <em> <em>DRAM_ECC_ERROR_COUNT</em> (2，0x80) register。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>超出阈值事件的 DRAM 可修正 ECC 错误计数</strong></td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left"><p>来自 NVDIMM-N 模块的平台检测到的可更正 ECC 阈值-超出事件数。</p>
<p>平台应将此值写入 <em></em> DRAM_THRESHOLD_ECC_COUNT </em> (2 0x81) register。</p></td>
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
<td align="left"><p>有关详细信息，请参阅 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a> 。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[获取 NVDIMM-N 运行状况信息（功能索引 11）](get-nvdimm-n-health-info--function-index-11-.md)

[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






