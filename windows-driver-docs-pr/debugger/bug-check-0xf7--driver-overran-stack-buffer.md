---
title: Bug 检查 0xF7 DRIVER_OVERRAN_STACK_BUFFER
description: DRIVER_OVERRAN_STACK_BUFFER bug 检查的值为0x000000F7。 这表明驱动程序已溢出基于堆栈的缓冲区。
keywords:
- Bug 检查 0xF7 DRIVER_OVERRAN_STACK_BUFFER
- DRIVER_OVERRAN_STACK_BUFFER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_OVERRAN_STACK_BUFFER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8c8d86f0d0660ffa058b278e06c34829eb2a0da3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827353"
---
# <a name="bug-check-0xf7-driver_overran_stack_buffer"></a>Bug 检查0xF7：驱动程序 \_ OVERRAN \_ 堆栈 \_ 缓冲区


驱动程序 \_ OVERRAN \_ 堆栈 \_ 缓冲区 bug 检查的值为0x000000F7。 这表明驱动程序已溢出基于堆栈的缓冲区。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="driver_overran_stack_buffer-parameters"></a>驱动程序 \_ OVERRAN \_ 堆栈 \_ 缓冲参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>堆栈中的实际安全检查 cookie</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>预期的安全检查 cookie</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预期安全检查 cookie 的位补码</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

驱动程序 overran 基于堆栈的缓冲区 (或局部变量) 的方式将覆盖函数的返回地址，并在函数返回时跳回到任意地址。

这是典型的 "缓冲区溢出" 黑客攻击。 系统已关闭，以防止恶意用户完全控制它。

<a name="resolution"></a>解决方法
----------

使用 [**kb (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令获取堆栈跟踪。

在缓冲区溢出处理程序和 bug 检查调用之前，堆栈上的最后一个例程是 overran 其局部变量的。

 

 




