---
title: 获取关键的运行状况信息（功能索引 10）
description: 此函数返回与运行状况相关的重要信息。
ms.assetid: 2083628D-FB46-4104-9F70-F7124B35DD04
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 019203df61baec312c465bdb82e302477b94bb8d
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851323"
---
# <a name="get-critical-health-info-function-index-10"></a>获取关键的运行状况信息（功能索引 10）


此函数返回与运行状况相关的重要信息。 调用[获取 Nvdimm-n 健康信息（Function index 11）](get-nvdimm-n-health-info--function-index-11-.md) ，并[获取能源源运行状况信息（功能索引12）](get-energy-source-health-info--function-index-12-.md)以获取更多与运行状况相关的信息。

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
<td align="left"><strong>关键运行状况信息</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>有关 NVDIMM-N 模块的任何问题的高级状态报告。</p>
<p>* Byte 0 – <em>MODULE_HEALTH</em> （0，0xA0）</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[获取 NVDIMM-N 运行状况信息（功能索引 11）](get-nvdimm-n-health-info--function-index-11-.md)

[获取能量源运行状况信息（功能索引 12）](get-energy-source-health-info--function-index-12-.md)

[\_用于字节寻址的支持能源的函数类的 DSM 接口（Function Interface 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






