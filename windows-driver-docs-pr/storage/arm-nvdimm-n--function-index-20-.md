---
title: Arm NVDIMM-N（功能索引 20）
description: 有关此函数的手臂 NVDIMM N 保存发生断电时的操作。
ms.assetid: 15D21B5A-2320-4C22-9957-ECC0EB46B02E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 68d4792fdc244f1d5ca998792b785a05fbb89d8b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357645"
---
# <a name="span-idstoragearmnvdimm-nfunctionindex20spanarm-nvdimm-n-function-index-20"></a><span id="storage.arm_nvdimm-n__function_index_20_"></span>Arm NVDIMM N （函数索引 20）


有关此函数的手臂 NVDIMM N 保存发生断电时的操作。 平台负责选择相应的保存的触发器。

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
<td align="left"><p>此函数可返回以下特定于函数的错误代码：</p>
<p>1：操作已超时。</p>
<p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Interface for Byte Addressable Energy Backed Function Class (Function Interface 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 字节可寻址能源支持的函数类 (函数接口 1) 的接口</a>有关信息。</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!请注意\]    &gt;这是一个同步函数。 它将返回仅当 arm 操作已完成或超时。如果该操作花费的时间超过超时值中定义\* *ARM\_TIMEOUT0* （0，0x20） 和\* *ARM\_TIMEOUT1* （0，0x21），该平台在返回之前，应中止此函数。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






