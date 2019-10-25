---
title: 输入缓冲区顺序示例 5
description: 输入缓冲区顺序示例 5
ms.assetid: f0ba80bb-ff84-4944-aae5-52eb0848edf5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0297d8bc8c3f7948eea48652b295ffebdd53d7b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840364"
---
# <a name="input-buffer-order-example-5"></a>输入缓冲区顺序示例 5


## <span id="ddk_input_buffer_order_example_5_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_5_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

VMR 启动对驱动程序的[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)函数的调用，以在[输入缓冲区顺序示例 4](input-buffer-order-example-4.md)中使用设备，将2个视频 substreams 与渐进式视频流组合在一起。 即使没有必要在目标缓冲区中生成输出，VMR 仍会传递相同数量的渐进视频样本。 **LpBufferInfo**数组中的图面序列如下：

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

 

驱动程序可以忽略索引1和索引3处的图面，因为对于隔行扫描操作不需要它们。 在示例的[**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)结构的**SampleFormat**成员中，将渐进式示例标记为 DXVA\_SampleProgressiveFrame 标志。 子流示例标记有新的 DXVA\_SampleSubStream 标志。

 

 





