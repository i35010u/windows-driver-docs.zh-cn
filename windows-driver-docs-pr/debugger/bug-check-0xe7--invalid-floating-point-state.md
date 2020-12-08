---
title: Bug 检查 0xE7 INVALID_FLOATING_POINT_STATE
description: INVALID_FLOATING_POINT_STATE bug 检查的值为0x000000E7。 这表示线程的保存的浮点状态无效。
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
ms.openlocfilehash: 45ea1aaa3acb4d0202eed6db78ed7bd52a0be83b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793275"
---
# <a name="bug-check-0xe7-invalid_floating_point_state"></a>Bug 检查0xE7： \_ 浮点 \_ \_ 状态无效


无效的 \_ 浮点 \_ \_ 状态 bug 检查的值为0x000000E7。 这表示线程的保存的浮点状态无效。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="invalid_floating_point_state-parameters"></a>无效 \_ 的 \_ 浮点 \_ 状态参数


参数1指示验证失败的有效性。 未使用参数4。 其他参数的意义取决于参数1的值。

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
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>标志字段</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>保存的上下文标志字段无效。 未设置 FLOAT_SAVE_VALID，或者某些保留位为非零值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>保存的 IRQL</p></td>
<td align="left"><p>当前 IRQL</p></td>
<td align="left"><p>当前处理器的 IRQL 不同于保存浮点上下文的时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>拥有此浮点上下文的线程的保存地址</p></td>
<td align="left"><p>当前线程</p></td>
<td align="left"><p>保存的上下文不属于当前线程。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

在还原线程的以前保存的浮点状态时，发现状态无效。

参数1指示验证失败的有效性。

 

 




