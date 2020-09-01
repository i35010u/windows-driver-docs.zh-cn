---
title: 输入缓冲区顺序示例 5
description: 输入缓冲区顺序示例 5
ms.assetid: f0ba80bb-ff84-4944-aae5-52eb0848edf5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a054a2ad11cd34bc8644eb2afe8c3ed555d7d048
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064754"
---
# <a name="input-buffer-order-example-5"></a>输入缓冲区顺序示例 5


## <span id="ddk_input_buffer_order_example_5_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_5_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

VMR 启动对驱动程序的 [**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md) 函数的调用，以在 [输入缓冲区顺序示例 4](input-buffer-order-example-4.md) 中使用设备，将2个视频 substreams 与渐进式视频流组合在一起。 即使没有必要在目标缓冲区中生成输出，VMR 仍会传递相同数量的渐进视频样本。 **LpBufferInfo**数组中的图面序列如下：

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
<td align="left"><p>渐进式输入</p></td>
<td align="left"><p>T-1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [2]</p></td>
<td align="left"><p>渐进式输入</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo [3]</p></td>
<td align="left"><p>渐进式输入</p></td>
<td align="left"><p>T + 1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [4]</p></td>
<td align="left"><p>流</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo [5]</p></td>
<td align="left"><p>流</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 2</p></td>
</tr>
</tbody>
</table>

 

驱动程序可以忽略索引1和索引3处的图面，因为对于隔行扫描操作不需要它们。 渐进式样本在 \_ 示例的[**DXVA \_ VideoSample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)结构的**SampleFormat**成员中标记 DXVA SampleProgressiveFrame 标志。 子流示例标记有新的 DXVA \_ SampleSubStream 标志。

 

