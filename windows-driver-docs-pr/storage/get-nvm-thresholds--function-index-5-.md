---
title: 获取 NVM 阈值（功能索引 5）
description: 此函数返回生存期百分比警告和错误阈值，如果命中或超过此阈值，则表示 NVDIMM-N 出现问题。
ms.assetid: E243AF8B-D70A-4FEF-BB88-ED78C4883D42
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 648ead7aea1931b520f819cbbaaa9c4df83b7acf
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851454"
---
# <a name="get-nvm-thresholds-function-index-5"></a>获取 NVM 阈值（功能索引 5）


此函数返回生存期百分比警告和错误阈值，如果命中或超过此阈值，则表示 NVDIMM-N 出现问题。

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
<td align="left"><strong>NVM 生存期百分比警告阈值</strong></td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left"><p>非易失性内存生存期的警告阈值的百分比值。</p>
<p><em>Byte 0 – <em>NVM_LIFETIME_WARNING_THRESHOLD</em> （0，0x98）</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>NVM 生存期百分比错误阈值</strong></td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left"><p>非易失性内存生存期的错误阈值的百分比值。</p>
<p></em>Byte 0 – <em>NVM_LIFETIME_ERROR_THRESHOLD</em> （0，0x90）</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设置 NVM 生存期百分比警告阈值（功能索引 6）](set-nvm-lifetime-percentage-warning-threshold--function-index-6-.md)

[\_用于字节寻址的支持能源的函数类的 DSM 接口（Function Interface 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






