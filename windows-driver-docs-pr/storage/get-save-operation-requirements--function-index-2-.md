---
title: 获取保存操作要求（功能索引 2）
description: 此函数返回保存的硬件要求的信息操作。
ms.assetid: 502DAF89-F390-40A4-846C-C3B4DF3E505D
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 73350bb78925e11a1507e19e25c5cea67f174e0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569112"
---
# <a name="get-save-operation-requirements-function-index-2"></a>获取保存操作要求（功能索引 2）


此函数返回保存的硬件要求的信息操作。 此函数应为所有 Nvdimm-n 支持主机托管能源源 (ES) 策略，但如果设备支持设备管理 ES 策略和保存操作要求不可用，可能会返回故障状态成功。

&gt; \[!请注意\]    &gt;用一个星号标记所有寄存器 (\*) 字节可寻址能源支持接口规范中定义的寄存器。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>输入


### <a name="span-idarg3spanspan-idarg3spanspan-idarg3spanarg3"></a><span id="Arg3"></span><span id="arg3"></span><span id="ARG3"></span>Arg3

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
<p>1：NVDIMM N 不会报告保存操作要求。</p>
<p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>平均能源需求</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>保存有关所需的平均电源 （单位为毫瓦） 操作。</p>
<p><em>字节 0 – <em>CSAVE_POWER_REQ0</em> （0，0x29）</p>
<p></em>1 – 字节<em>CSAVE_POWER_REQ1</em> （0，0x2A）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>空闲处理能力要求</strong></td>
<td align="left">2</td>
<td align="left">6</td>
<td align="left"><p>（单位为毫瓦） 的平均电源模块需要在保存后操作完成。</p>
<p><em>字节 0 – <em>CSAVE_IDLE_POWER_REQ0</em> （0、 0x2B）</p>
<p></em>1 – 字节<em>CSAVE_IDLE_POWER_REQ1</em> （0、 0x2C）</p></td>
</tr>
<tr class="even">
<td align="left"><strong>最小电压要求</strong></td>
<td align="left">2</td>
<td align="left">8</td>
<td align="left"><p>最小电压 （用毫伏表示） ES 具有到服务在保存期间操作</p>
<p><em>Byte 0 – <em>CSAVE_MIN_VOLT_REQ0</em> (0, 0x2D)</p>
<p></em>Byte 1 – <em>CSAVE_MIN_VOLT_REQ1</em> (0, 0x2E)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>最大电压要求</strong></td>
<td align="left">2</td>
<td align="left">10</td>
<td align="left"><p>最大电压 （用毫伏表示） ES 具有到服务在保存期间操作</p>
<p><em>Byte 0 – <em>CSAVE_MAX_VOLT_REQ0</em> (0, 0x2F)</p>
<p></em>Byte 1 – <em>CSAVE_MAX_VOLT_REQ1</em> (0, 0x30)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






