---
title: 输入缓冲区顺序示例 3
description: 输入缓冲区顺序示例 3
ms.assetid: 627102bb-e7a8-4b6d-9a52-f8bf4b9727d6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4ea1e3299ef37febc5e68ce9402e1d899cdbefc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350260"
---
# <a name="input-buffer-order-example-3"></a>输入缓冲区顺序示例 3


## <span id="ddk_input_buffer_order_example_3_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_3_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

启动对驱动程序的调用时 VMR *DeinterlaceBltEx*函数，以使用中的设备[输入缓冲区顺序示例 1](input-buffer-order-example-1.md)和[输入缓冲区顺序示例 2](input-buffer-order-example-2.md)到改为3 个视频的子流结合渐进式视频流。 序列中的图面**lpBufferInfo**数组：

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
<td align="left"><p>T</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo[2]</p></td>
<td align="left"><p>子流</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[3]</p></td>
<td align="left"><p>子流</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo[4]</p></td>
<td align="left"><p>子流</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 3</p></td>
</tr>
</tbody>
</table>

 

在示例 2 到 3 个更改，从更改视频流交错到渐进式和其他视频子流成为活动状态。

 

 





