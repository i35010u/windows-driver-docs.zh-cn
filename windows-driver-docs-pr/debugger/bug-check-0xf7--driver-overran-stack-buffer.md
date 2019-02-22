---
title: Bug 检查 0xF7 DRIVER_OVERRAN_STACK_BUFFER
description: DRIVER_OVERRAN_STACK_BUFFER bug 检查具有 0x000000F7 值。 这表示一个驱动程序具有溢出基于堆栈的缓冲区。
ms.assetid: 5981b5e0-90c1-486e-8bbf-2778f2595f6b
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
ms.openlocfilehash: 91229266d64c82e2f860a21a1e1e782bb7d448b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526725"
---
# <a name="bug-check-0xf7-driveroverranstackbuffer"></a>Bug 检查 0xF7:驱动程序\_OVERRAN\_堆栈\_缓冲区


该驱动程序\_OVERRAN\_堆栈\_缓冲区 bug 检查的值为 0x000000F7。 这表示一个驱动程序具有溢出基于堆栈的缓冲区。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="driveroverranstackbuffer-parameters"></a>驱动程序\_OVERRAN\_堆栈\_缓冲区参数


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
<td align="left"><p>实际的安全检查 cookie 从堆栈</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>预计的安全检查 cookie</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预计的安全检查 cookie 位求补</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

驱动程序溢出本来会被覆盖函数的返回地址和该函数返回时，跳转回任意地址的方式基于堆栈的缓冲区 （或本地变量）。

这是一种典型"缓冲区溢出"黑客攻击。 系统已关闭以防止恶意用户获得完全控制。

<a name="resolution"></a>分辨率
----------

使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令来获取堆栈跟踪。

之前的缓冲区溢出处理程序和 bug 检查调用堆栈上的最后一个例程是溢出其本地变量。

 

 




