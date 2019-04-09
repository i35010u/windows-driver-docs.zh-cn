---
title: Bug 检查 0xE7 INVALID_FLOATING_POINT_STATE
description: INVALID_FLOATING_POINT_STATE bug 检查具有 0x000000E7 值。 这指示线程的已保存浮点状态无效。
ms.assetid: 71a61132-cb7f-4618-b3d5-95602e52c098
keywords:
- Bug 检查 0xE7 INVALID_FLOATING_POINT_STATE
- INVALID_FLOATING_POINT_STATE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_FLOATING_POINT_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bfd6786c9d4b66663d91758ebfa7bd8a46e60399
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239816"
---
# <a name="bug-check-0xe7-invalidfloatingpointstate"></a>Bug 检查 0xE7：无效\_浮动\_点\_状态


无效\_浮动\_点\_状态 bug 检查的值为 0x000000E7。 这指示线程的已保存浮点状态无效。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="invalidfloatingpointstate-parameters"></a>无效\_浮动\_点\_状态参数


参数 1 指示哪些有效性检查失败。 不使用参数 4。 其他参数的含义取决于参数 1 的值。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>标志字段</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已保存的上下文标志字段无效。 未设置 FLOAT_SAVE_VALID，或者某些保留的位均为非零值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>已保存的 IRQL</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>当前处理器的 IRQL 不是与浮点上下文已保存时相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>拥有此浮点上下文的线程的已保存的地址</p></td>
<td align="left"><p>当前线程</p></td>
<td align="left"><p>已保存的上下文不属于当前线程。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

时还原以前保存浮点状态的线程时，发现状态无效。

参数 1 指示哪些有效性检查失败。

 

 




