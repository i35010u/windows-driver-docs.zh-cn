---
title: 设置内存错误计数器（功能索引 31）
description: 此函数将跟踪对调用方指定的值可纠正和无法纠正的内存错误事件的计数器。 此函数的用途是启用软件验证。
ms.assetid: 0EC4B442-902B-4589-A831-9637F4D60F86
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 60d21eb2395e2ccdac11ec39b1f71c2044b74527
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329977"
---
# <a name="set-memory-error-counters-function-index-31"></a>设置内存错误计数器（功能索引 31）


此函数将跟踪对调用方指定的值可纠正和无法纠正的内存错误事件的计数器。 此函数的用途是启用软件验证。

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
<td align="left"><strong>DRAM 无法纠正的 ECC 错误的计数</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>检测到的平台从 NVDIMM N 模块无法纠正 ECC 错误数。</p>
<p>平台应写入此值设置为<em> <em>DRAM_ECC_ERROR_COUNT</em> （2，0x80） 注册。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>上面阈值事件 DRAM 可纠正的 ECC 错误的计数</strong></td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left"><p>可纠正 ECC-超过阈值的事件数检测到 NVDIMM N 模块中的平台。</p>
<p>平台应写入此值设置为 DRAM_THRESHOLD_ECC_COUNT</em> （2，0x81） 注册。</p></td>
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
<td align="left"><p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关详细信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[获取 NVDIMM N 运行状况信息 （函数索引 11）](get-nvdimm-n-health-info--function-index-11-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






