---
title: 输入的缓冲区顺序示例 1
description: 输入的缓冲区顺序示例 1
ms.assetid: 1fd5f181-8bf7-4b16-adc9-ed751f9ad664
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5121bc7c489dceb4a4d6679c5c6fb88676d1f5d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519017"
---
# <a name="input-buffer-order-example-1"></a>输入的缓冲区顺序示例 1


## <span id="ddk_input_buffer_order_example_1_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_1_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

请考虑不需要任何上一输出参考帧或旧或更新输入的参考帧来执行其取消隔行扫描操作的设备 (例如， [bob deinterlacer](bob-deinterlacing.md))。 序列中的图面**lpBufferInfo**此设备的数组：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">索引位置</th>
<th align="left">图面上的类型</th>
<th align="left">临时位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>lpBufferInfo[0]</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>T</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo[1]</p></td>
<td align="left"><p>交错的输入</p></td>
<td align="left"><p>T</p></td>
</tr>
</tbody>
</table>

 

 

 





