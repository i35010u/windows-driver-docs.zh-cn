---
title: Arm NVDIMM-N（功能索引 20）
description: 此功能在断电时对 NVDIMM-N 进行操作，以便保存操作。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8353c304d72f039ba2594f6e865a1cfe94df92b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811805"
---
# <a name="span-idstoragearm_nvdimm-n__function_index_20_spanarm-nvdimm-n-function-index-20"></a><span id="storage.arm_nvdimm-n__function_index_20_"></span>Arm NVDIMM-N（功能索引 20）


此功能在断电时对 NVDIMM-N 进行操作，以便保存操作。 平台负责选择适当的保存触发器。

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
<td align="left"><p>此函数可能返回以下 Function-Specific 错误代码：</p>
<p>1：操作超时。</p>
<p>有关信息，请参阅 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Interface for Byte Addressable Energy Backed Function Class (Function Interface 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)"> (函数接口 1) 的 _DSM 接口获取用于字节可寻址的支持功能的函数类 </a> 。</p></td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> 这是一个同步函数。 仅当 arm 操作完成或超时时，它才会返回。如果操作所用的时间超过 \* *ARM \_ TIMEOUT0* (0，0x20) 和 \* *arm \_ TIMEOUT1* (0，0x21) ，该平台应在返回前中止此函数。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[\_用于字节寻址的支持能源的函数类 (函数接口 1) 的 DSM 接口 ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






