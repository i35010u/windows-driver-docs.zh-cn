---
title: Bug 检查 0x153 KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION
description: KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION bug 检查的值为0x00000153。 这指示线程在释放其所有 AutoBoost 锁条目之前已终止。
keywords:
- Bug 检查 0x153 KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION
- KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_LOCK_ENTRY_LEAKED_ON_THREAD_TERMINATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9e9d93fd1a4a85268b317872cac3a59030f9d174
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830803"
---
# <a name="bug-check-0x153-kernel_lock_entry_leaked_on_thread_termination"></a>Bug 检查0x153： \_ \_ \_ \_ \_ 线程 \_ 终止时泄漏内核锁定条目


\_ \_ \_ \_ \_ 线程终止 BUG 检查上泄漏的内核锁定条目的 \_ 值为0x00000153。 这指示线程在释放其所有 AutoBoost 锁条目之前已终止。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="kernel_lock_entry_leaked_on_thread_termination-parameters"></a>\_ \_ \_ \_ \_ 线程终止参数上泄漏的 \_ 内核锁定条目


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
<td align="left">线程的地址</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">未释放的项的地址</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left"><p>指示条目状态的状态代码</p>
<p>0x1：锁定指针不为 NULL</p>
<p>0x2：已设置线程指针保留位</p>
<p>0x3：线程指针已损坏</p>
<p>0x4：该项的剩余 IO 或 CPU 提升剩余</p></td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">预留</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

通常，当某个线程从未释放它以前获取的锁定时，这种情况通常会导致 (例如，通过依赖另一个线程将其释放) ，或者线程未提供一致的标志集来锁定包 Api。

 

 




