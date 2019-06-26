---
title: Bug 检查 0xCF TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE
description: TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE bug 检查具有 0x000000CF 值。 这表示一个驱动程序被错误地移植到终端服务器。
ms.assetid: 1c3351d8-95df-4a12-a9c5-36aa6a5cf236
keywords:
- Bug 检查 0xCF TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE
- TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- TERMINAL_SERVER_DRIVER_MADE_INCORRECT_MEMORY_REFERENCE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a653de117ab5069e8894ba2020e30d3010ee0f32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367163"
---
# <a name="bug-check-0xcf-terminalserverdrivermadeincorrectmemoryreference"></a>Bug 检查 0xCF：终端\_服务器\_驱动程序\_所做\_不正确\_内存\_引用


在终端\_服务器\_驱动程序\_所做\_不正确\_内存\_引用 bug 检查的值为 0x000000CF。 这表示一个驱动程序被错误地移植到终端服务器。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="terminalserverdrivermadeincorrectmemoryreference-parameters"></a>终端\_服务器\_驱动程序\_所做\_不正确\_内存\_引用参数


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
<td align="left"><p>引用的内存地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>写入</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>（如果已知） 引用内存的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) **KiBugCheckDriver**。

<a name="cause"></a>原因
-----

该驱动程序从系统进程上下文中引用会话空间地址。 这可能会从队列到系统工作线程的项的驱动程序。

此驱动程序需要遵循的终端服务器的内存管理规则。

 

 




