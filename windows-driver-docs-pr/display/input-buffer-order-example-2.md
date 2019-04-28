---
title: 输入缓冲区顺序示例 2
description: 输入缓冲区顺序示例 2
ms.assetid: e480bd93-4ae2-4a6c-b669-69c44c0154d0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3a637b335544acce6b32cf1daacdb23897359e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350233"
---
# <a name="input-buffer-order-example-2"></a>输入缓冲区顺序示例 2


## <span id="ddk_input_buffer_order_example_2_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_2_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

启动对驱动程序的调用时 VMR [ **DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563927)函数，以使用中的设备[输入缓冲区顺序示例 1](input-buffer-order-example-1.md)来组合和交错 2 个视频的子流视频流。 序列中的图面**lpBufferInfo**数组：

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
<td align="left"><p>交错的输入</p></td>
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
</tbody>
</table>

 

 

 





