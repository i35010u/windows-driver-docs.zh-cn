---
title: 输入缓冲区顺序示例 3
description: 输入缓冲区顺序示例 3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f09695c3c099300bb573d021eb3d2d6d67ba4ffd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827241"
---
# <a name="input-buffer-order-example-3"></a>输入缓冲区顺序示例 3


## <span id="ddk_input_buffer_order_example_3_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_3_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

VMR 启动对驱动程序的 *DeinterlaceBltEx* 函数的调用，以在 [输入缓冲区顺序示例 1](input-buffer-order-example-1.md) 中使用设备， [并将](input-buffer-order-example-2.md) 3 个视频 substreams 与渐进式视频流组合在一起。 **LpBufferInfo** 数组中的图面序列如下：

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
<td align="left"><p>T</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [2]</p></td>
<td align="left"><p>流</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 1</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo [3]</p></td>
<td align="left"><p>流</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo [4]</p></td>
<td align="left"><p>流</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Z + 3</p></td>
</tr>
</tbody>
</table>

 

在从示例2到3的更改中，视频流从交错更改为渐进，其他视频子流变为活动状态。

 

 





