---
title: Bug 检查 0xE1 WORKER_THREAD_RETURNED_AT_BAD_IRQL
description: WORKER_THREAD_RETURNED_AT_BAD_IRQL bug 检查的值为0x000000E1。 这表明工作线程已完成并返回，并 DISPATCH_LEVEL IRQL。
keywords:
- Bug 检查 0xE1 WORKER_THREAD_RETURNED_AT_BAD_IRQL
- WORKER_THREAD_RETURNED_AT_BAD_IRQL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_AT_BAD_IRQL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 65021101e634b6a12f68b18f201e2bbf8bfeedd2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816407"
---
# <a name="bug-check-0xe1-worker_thread_returned_at_bad_irql"></a>Bug 检查0xE1： \_ \_ \_ \_ 错误的 IRQL 返回的 \_ 工作线程


错误的 \_ \_ \_ IRQL bug 检查返回的工作线程的 \_ \_ 值为0x000000E1。 这表明工作线程已完成并返回，其 IRQL &gt; = 调度 \_ 级别。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="worker_thread_returned_at_bad_irql-parameters"></a>工作 \_ 线程 \_ \_ 在 \_ 错误的 \_ IRQL 参数上返回


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
<td align="left"><p>辅助角色例程的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>工作线程返回的 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>工作项参数</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>工作项地址</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

工作线程已完成并返回，其 IRQL &gt; = 调度 \_ 级别。

<a name="resolution"></a>解决方法
----------

若要查找导致错误的驱动程序，请使用 [**ln (列出最接近)**](ln--list-nearest-symbols-.md) 调试器命令的符号：

```dbgcmd
kd> ln address
```

其中 *address* 是在参数1中给定的辅助进程例程地址。

 

 




