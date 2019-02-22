---
title: 输入的缓冲区顺序示例 5
description: 输入的缓冲区顺序示例 5
ms.assetid: f0ba80bb-ff84-4944-aae5-52eb0848edf5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f61909e55eaf370fffe958f70998ea9eac8ce59b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525892"
---
# <a name="input-buffer-order-example-5"></a>输入的缓冲区顺序示例 5


## <span id="ddk_input_buffer_order_example_5_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_5_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

VMR 开始，驱动程序的调用[ **DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563927)函数，以使用中的设备[输入缓冲区顺序示例 4](input-buffer-order-example-4.md)组合使用 2 个视频的子流渐进式视频流。 VMR 仍然通过渐进式视频样本的数量，即使这些示例不需要生成目标缓冲区中的输出。 序列中的图面**lpBufferInfo**数组：

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
<th align="left">图面上的类型</th>
<th align="left">临时位置</th>
<th align="left">层位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>lpBufferInfo[0]</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>T</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[1]</p></td>
<td align="left"><p>渐进式输入</p></td>
<td align="left"><p>T - 1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo[2]</p></td>
<td align="left"><p>渐进式输入</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[3]</p></td>
<td align="left"><p>渐进式输入</p></td>
<td align="left"><p>T + 1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo[4]</p></td>
<td align="left"><p>子流</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[5]</p></td>
<td align="left"><p>子流</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 2</p></td>
</tr>
</tbody>
</table>

 

该驱动程序可以忽略索引 1 和索引 3 处的图面，因为它们不是取消隔行扫描操作所必需的。 渐进式示例都标有 DXVA\_SampleProgressiveFrame 标志**SampleFormat**的成员[ **DXVA\_VideoSample2** ](https://msdn.microsoft.com/library/windows/hardware/ff564092)结构的示例。 子流示例都标有新 DXVA\_SampleSubStream 标志。

 

 





