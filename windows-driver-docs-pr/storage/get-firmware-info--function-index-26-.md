---
title: 获取固件信息 （函数索引 26）
description: 此函数检索有关固件映像槽的信息。
ms.assetid: ABE67651-6351-4D8E-BCFF-0488D2A34DC5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 131dd2bfe35d3abb3164943835ebe578b8982f58
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547488"
---
# <a name="get-firmware-info-function-index-26"></a>获取固件信息 （函数索引 26）


此函数检索有关固件映像槽的信息。 调用[获取 NVDIMM N 标识 (函数索引 1)](get-nvdimm-n-identification--function-index-1-.md)来检索当前的槽数。

&gt; \[!请注意\]    &gt;用一个星号标记所有寄存器 (\*) 字节可寻址能源支持接口规范中定义的寄存器。

 

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
<td align="left"><strong>个固件插槽</strong></td>
<td align="left">1</td>
<td align="left">0</td>
<td align="left"><p>报告其信息的固件映像槽。</p></td>
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
<td align="left"><p>转到<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM 方法输出</a>有关信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>版本</strong></td>
<td align="left">2</td>
<td align="left">4</td>
<td align="left"><p>在指定槽中的固件映像的固件版本。</p>
<p><em>Byte 0 – <em>SLOTX_FWVER0</em> (0, 0x07/0x09)</p>
<p></em>Byte 1 – <em>SLOTX_FWVER1</em> (0, 0x08/0x0A)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[启动固件更新 （函数索引 22）](start-firmware-update--function-index-22-.md)

[发送固件更新数据 （函数索引 23）](send-firmware-update-data--function-index-23-.md)

[完成固件更新 （函数索引 24）](finish-firmware-update--function-index-24-.md)

[选择固件映像槽 （函数索引 25）](select-firmware-image-slot--function-index-25-.md)

[\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






