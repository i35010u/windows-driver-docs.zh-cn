---
title: Bug 检查 0x15C PDC_WATCHDOG_TIMEOUT_LIVEDUMP
description: "\"PDC_WATCHDOG_TIMEOUT_LIVEDUMP bug 检查\" 的值为 \"0x0000015C\"，指示系统组件无法响应，阻止进入或退出连接待机。"
keywords:
- Bug 检查 0x15C PDC_WATCHDOG_TIMEOUT_LIVEDUMP
- PDC_WATCHDOG_TIMEOUT_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PDC_WATCHDOG_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 54fe9d731fc9ee8c7f8e8eb721f130fb4f73cc23
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830793"
---
# <a name="bug-check-0x15c-pdc_watchdog_timeout_livedump"></a>Bug 检查0x15C： PDC \_ 监视程序 \_ 超时 \_ LIVEDUMP


PDC \_ 监视程序 \_ 超时 \_ LIVEDUMP bug 检查的值为0x0000015C。 这表示系统组件未能在分配的时间段内响应，从而导致系统进入或退出连接待机状态。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="pdc_watchdog_timeout_livedump-parameters"></a>PDC \_ 监视程序 \_ 超时 \_ LIVEDUMP 参数


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
<td align="left">1</td>
<td align="left">挂起组件的客户端 ID。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><p>挂起组件的客户端类型。</p>
0x1：通知客户端未能响应。
<p>3-指向通知客户端 (pdc！ _PDC_NOTIFICATION_CLIENT) 的指针。</p>
<p>4-指向 pdc！PDC_14F_TRIAGE 结构。</p>
0x2：复原客户端未能响应。
<p>3-指向复原客户端 (pdc！ _PDC_RESILIENCY_CLIENT) 的指针。</p>
<p>4-指向 pdc！PDC_14F_TRIAGE 结构。</p>
0x3：激活器客户端持有引用的时间太长
<p>3-指向激活客户端 (pdc！ _PDC_ACTIVATOR_CLIENT) 的指针。</p>
<p>4-指向 pdc！PDC_14F_TRIAGE 结构。</p></td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数2</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数2</td>
</tr>
</tbody>
</table>

 

 

 




