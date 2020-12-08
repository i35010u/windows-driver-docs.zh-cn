---
title: Bug 检查 0x101 CLOCK_WATCHDOG_TIMEOUT
description: "\"CLOCK_WATCHDOG_TIMEOUT bug 检查\" 的值为0x00000101，指示在分配的时间间隔内未收到辅助处理器上的预期时钟中断。"
keywords:
- Bug 检查 0x101 CLOCK_WATCHDOG_TIMEOUT
- CLOCK_WATCHDOG_TIMEOUT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CLOCK_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 38c7f1a2196d16effd708f76fa1a2d71e812527b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803637"
---
# <a name="bug-check-0x101-clock_watchdog_timeout"></a>Bug 检查0x101：时钟 \_ 监视程序 \_ 超时


时钟 \_ 监视程序 \_ 超时 bug 检查的值为0x00000101。 这表示在分配的时间间隔内未接收到多处理器系统中的辅助处理器上的预期时钟中断。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="clock_watchdog_timeout-parameters"></a>时钟 \_ 监视程序 \_ 超时参数


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
<td align="left"><p>时钟中断超时间隔，以名义时钟计时周期为单位</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>处理器控制块的地址 (无响应处理器的 PRCB) </p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

指定的处理器未处理中断。 通常，当处理器无响应或死锁时，会发生这种情况。

 

 




