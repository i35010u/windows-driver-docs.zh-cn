---
title: 获取 NVDIMM-N 运行状况信息（功能索引 11）
description: 此函数返回有关 NVDIMM-N 模块的运行状况的信息。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dd25d15d8cf752e09305ea70393b82ab7a895531
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835287"
---
# <a name="span-idstorageget_nvdimm-n_health_info__function_index_11_spanget-nvdimm-n-health-info-function-index-11"></a><span id="storage.get_nvdimm-n_health_info__function_index_11_"></span>获取 NVDIMM-N 运行状况信息（功能索引 11）


此函数返回有关 NVDIMM-N 模块的运行状况的信息。

> [!NOTE]
> 标记为星形 () 的所有寄存器 \* 都是在可通过字节可寻址的、支持电源的接口规范中定义的寄存器。

 

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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状态</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>请参阅 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a> 获取详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>模块运行状况</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>有关 NVDIMM-N 模块的运行状况的详细信息。</p>
<p><em>Byte 0 – <em>MODULE_HEALTH_STATUS0 (</em>) </p>
<p></em>字节1– <em>MODULE_HEALTH_STATUS1</em> (0，0xA2) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>模块当前温度</strong></td>
<td align="left">2</td>
<td align="left">6</td>
<td align="left"><p>模块温度（摄氏度）。 最小值为0</p>
.
<p>此信息是从 NVDIMM-N 的串行存在检测 EEPROM 上的温度传感器中检索的。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>错误阈值状态</strong></td>
<td align="left">1</td>
<td align="left">8</td>
<td align="left"><p>有关 NVDIMM-N 模块上的错误阈值的状态。</p>
<p><em>Byte 0 – <em>ERROR_THRESHOLD_STATUS (</em>) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>警告阈值状态</strong></td>
<td align="left">1</td>
<td align="left">9</td>
<td align="left"><p>有关 NVDIMM-N 模块上的警告阈值的状态。</p>
<p></em>Byte 0 – <em>WARNING_THRESHOLD_STATUS (</em>) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>NVM 生存期</strong></td>
<td align="left">1</td>
<td align="left">10</td>
<td align="left"><p>上一个已知的非易失性内存生存期百分比值。</p>
<p><em>Byte 0 – <em>NVM_LIFETIME (</em>) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>DRAM 无法纠正的 ECC 错误计数</strong></td>
<td align="left">1</td>
<td align="left">11</td>
<td align="left"><p>平台从 NVDIMM-N 模块检测到的无法纠正的 ECC 错误数。</p>
<p></em>Byte 0 – <em>DRAM_ECC_ERROR_COUNT</em> (2，0x80) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>超出阈值事件的 DRAM 可修正 ECC 错误计数</strong></td>
<td align="left">1</td>
<td align="left">12</td>
<td align="left"><p>来自 NVDIMM-N 模块的平台检测到的可更正 ECC 阈值-超出事件数。</p>
<p>* Byte 0 – <em>DRAM_THRESHOLD_ECC_COUNT</em> (2) </p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[获取关键的运行状况信息（功能索引 10）](get-critical-health-info--function-index-10-.md)

[获取能量源运行状况信息（功能索引 12）](get-energy-source-health-info--function-index-12-.md)

[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






