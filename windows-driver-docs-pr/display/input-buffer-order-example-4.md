---
title: 输入的缓冲区顺序示例 4
description: 输入的缓冲区顺序示例 4
ms.assetid: 56370370-4786-44e4-9447-3937e4595e27
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69293f3be29a822eb087a62b41e3d1d0c0507d9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554065"
---
# <a name="input-buffer-order-example-4"></a>输入的缓冲区顺序示例 4


## <span id="ddk_input_buffer_order_example_4_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_4_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

需要单个向后引用示例、 单个供将来参考示例中和当前的示例，若要执行的更复杂取消隔行扫描设备，请考虑其取消隔行扫描操作。 两个视频的子流也是与取消隔行扫描操作结合使用。 序列中的图面**lpBufferInfo**数组：

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
<td align="left"><p>T - 1</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="odd">
<td align="left"><p>lpBufferInfo[2]</p></td>
<td align="left"><p>交错的输入</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>Z</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[3]</p></td>
<td align="left"><p>交错的输入</p></td>
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

 

 

 





