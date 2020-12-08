---
title: 输入缓冲区顺序示例 6
description: 输入缓冲区顺序示例 6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 178c66a64f4f930d0880e3ee50b0e4f8f3dfe832
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839295"
---
# <a name="input-buffer-order-example-6"></a>输入缓冲区顺序示例 6


## <span id="ddk_input_buffer_order_example_6_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_6_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

请考虑使用更复杂的隔行扫描设备，该设备需要两个以前的输出帧、单个向后引用示例、一个将来的引用示例，以及用于执行取消隔行扫描操作的当前示例。 两个视频 substreams 也与隔行扫描操作组合在一起。 **LpBufferInfo** 数组中的图面序列如下：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">索引位置</th>
<th align="left">Surface 类型</th>
<th align="left">临时位置</th>
<th align="left">层位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>lpBufferInfo [0]</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>T</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo [1]</p></td>
<td align="left"><p>上一个目标</p></td>
<td align="left"><p>T-1</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [2]</p></td>
<td align="left"><p>上一个目标</p></td>
<td align="left"><p>T-2</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo [3]</p></td>
<td align="left"><p>隔行扫描输入</p></td>
<td align="left"><p>T-1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [4]</p></td>
<td align="left"><p>隔行扫描输入</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo [5]</p></td>
<td align="left"><p>隔行扫描输入</p></td>
<td align="left"><p>T + 1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [6]</p></td>
<td align="left"><p>流</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo [7]</p></td>
<td align="left"><p>流</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 2</p></td>
</tr>
</tbody>
</table>

 

 

 





