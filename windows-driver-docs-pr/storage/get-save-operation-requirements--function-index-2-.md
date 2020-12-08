---
title: 获取保存操作要求（功能索引 2）
description: 此函数返回有关保存操作的硬件要求的信息。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5ab3c18bf553124a330726b149ba7c3a14a1213d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835265"
---
# <a name="get-save-operation-requirements-function-index-2"></a>获取保存操作要求（功能索引 2）


此函数返回有关保存操作的硬件要求的信息。 此函数应成功满足所有支持主机托管的能源源 (ES) 策略的 NVDIMM-Ns，但如果设备支持设备托管的 ES 策略并且保存操作要求不可用，则可能会返回失败状态。

> [!NOTE]
> 标记为星形 () 的所有寄存器 \* 都是在可通过字节可寻址的、支持电源的接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>送


### <a name="span-idarg3spanspan-idarg3spanspan-idarg3spanarg3"></a><span id="Arg3"></span><span id="arg3"></span><span id="ARG3"></span>Arg3

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
<td align="left"><p>此函数可能返回以下 Function-Specific 错误代码：</p>
<p>1： NVDIMM-N 不会报告保存操作要求。</p>
<p>有关详细信息，请参阅 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>平均电源要求</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>保存操作所需的毫瓦) 的平均功率 (。</p>
<p><em>Byte 0 – <em>CSAVE_POWER_REQ0 (</em>) </p>
<p></em>字节1– <em>CSAVE_POWER_REQ1</em> (0，0x2A) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>空闲电源要求</strong></td>
<td align="left">2</td>
<td align="left">6</td>
<td align="left"><p>完成保存操作后，模块) 毫瓦中的平均电源 (。</p>
<p><em>Byte 0 – <em>CSAVE_IDLE_POWER_REQ0 (</em>) </p>
<p></em>字节1– <em>CSAVE_IDLE_POWER_REQ1</em> (0，0x2C) </p></td>
</tr>
<tr class="even">
<td align="left"><strong>最低电压要求</strong></td>
<td align="left">2</td>
<td align="left">8</td>
<td align="left"><p>在保存操作期间，ES) ES 必须服务的最低电压 (</p>
<p><em>Byte 0 – <em>CSAVE_MIN_VOLT_REQ0 (</em>) </p>
<p></em>字节1– <em>CSAVE_MIN_VOLT_REQ1</em> (0，0x2E) </p></td>
</tr>
<tr class="odd">
<td align="left"><strong>最大电压要求</strong></td>
<td align="left">2</td>
<td align="left">10</td>
<td align="left"><p>在保存操作期间，ES) ES 必须服务的最大电压 (</p>
<p><em>Byte 0 – <em>CSAVE_MAX_VOLT_REQ0 (</em>) </p>
<p></em>字节1– <em>CSAVE_MAX_VOLT_REQ1</em> (0，0x30) </p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






