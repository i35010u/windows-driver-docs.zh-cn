---
title: 输入缓冲区顺序示例 1
description: 输入缓冲区顺序示例 1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 872d4529f5abbd596c5b41e3823448e59020d021
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827249"
---
# <a name="input-buffer-order-example-1"></a>输入缓冲区顺序示例 1


## <span id="ddk_input_buffer_order_example_1_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_EXAMPLE_1_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

假设某个设备不需要任何以前的输出引用帧，或者以前或将来的输入引用帧来执行其取消隔行扫描操作 (例如， [bob deinterlacer](bob-deinterlacing.md)) 。 此设备的 **lpBufferInfo** 数组中的表面序列如下：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">索引位置</th>
<th align="left">Surface 类型</th>
<th align="left">临时位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>lpBufferInfo [0]</p></td>
<td align="left"><p>目标</p></td>
<td align="left"><p>T</p></td>
</tr>
<tr class="even">
<td align="left"><p>lpBufferInfo [1]</p></td>
<td align="left"><p>隔行扫描输入</p></td>
<td align="left"><p>T</p></td>
</tr>
</tbody>
</table>

 

 

 





