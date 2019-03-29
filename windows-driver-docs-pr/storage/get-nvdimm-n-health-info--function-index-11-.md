---
title: 获取 NVDIMM-N 运行状况信息（功能索引 11）
description: 此函数返回 NVDIMM N 模块的运行状况的信息。
ms.assetid: E0FCC4C6-31CB-4D46-ADCE-99EBA2BFF798
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ddadffd117fad3f731e3cd2f64f56c1ad11a397d
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348808"
---
# <a name="span-idstoragegetnvdimm-nhealthinfofunctionindex11spanget-nvdimm-n-health-info-function-index-11"></a><span id="storage.get_nvdimm-n_health_info__function_index_11_"></span>获取 NVDIMM N 运行状况信息 （函数索引 11）


此函数返回 NVDIMM N 模块的运行状况的信息。

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
<td align="left"><strong>模块运行状况</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>详细了解 NVDIMM N 模块的运行状况。</p>
<p><em>字节 0 – <em>MODULE_HEALTH_STATUS0</em> （0，0xA1）</p>
<p></em>1 – 字节<em>MODULE_HEALTH_STATUS1</em> （0，0xA2）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>模块当前温度</strong></td>
<td align="left">2</td>
<td align="left">6</td>
<td align="left"><p>模块温度以摄氏度。 最小值为 0</p>
.
<p>从温度传感器 NVDIMM N 串行存在检测 EEPROM 上检索此信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>错误阈值状态</strong></td>
<td align="left">1</td>
<td align="left">8</td>
<td align="left"><p>有关 NVDIMM N 模块上的错误阈值的状态。</p>
<p><em>字节 0 – <em>ERROR_THRESHOLD_STATUS</em> （0，0xA5）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>警告阈值状态</strong></td>
<td align="left">1</td>
<td align="left">9</td>
<td align="left"><p>有关 NVDIMM N 模块上的警告阈值的状态。</p>
<p></em>字节 0 – <em>WARNING_THRESHOLD_STATUS</em> （0，0xA7）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>NVM 生存期</strong></td>
<td align="left">1</td>
<td align="left">10</td>
<td align="left"><p>最后一个已知的非易失性内存生存期百分比值。</p>
<p><em>字节 0 – <em>NVM_LIFETIME</em> （0，0xC0）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>DRAM 无法纠正的 ECC 错误的计数</strong></td>
<td align="left">1</td>
<td align="left">11</td>
<td align="left"><p>检测到的平台从 NVDIMM N 模块无法纠正 ECC 错误数。</p>
<p></em>字节 0 – <em>DRAM_ECC_ERROR_COUNT</em> （2，0x80）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>上面阈值事件 DRAM 可纠正的 ECC 错误的计数</strong></td>
<td align="left">1</td>
<td align="left">12</td>
<td align="left"><p>可纠正 ECC-超过阈值的事件数检测到 NVDIMM N 模块中的平台。</p>
<p>* 字节 0 – <em>DRAM_THRESHOLD_ECC_COUNT</em> （2，0x81）</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[获取关键运行状况信息 （函数索引 10）](get-critical-health-info--function-index-10-.md)

[获取能源源运行状况信息 （函数索引 12）](get-energy-source-health-info--function-index-12-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






