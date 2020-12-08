---
title: Bug 检查 0x1C5 IO_THREADPOOL_DEADLOCK_LIVEDUMP
description: IO_THREADPOOL_DEADLOCK_LIVEDUMP bug 检查的值为0x000001C5。 这表示内核模式 threadpool 遇到死锁情况。
keywords:
- Bug 检查 0x1C5 IO_THREADPOOL_DEADLOCK_LIVEDUMP
- IO_THREADPOOL_DEADLOCK_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IO_THREADPOOL_DEADLOCK_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 73e5932dcde8f4a6d8b33b8da940b342eb1c8dcd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836889"
---
# <a name="bug-check-0x1c5-io_threadpool_deadlock_livedump"></a>Bug 检查0x1C5： IO \_ 线程 \_ 死锁 \_ LIVEDUMP


IO \_ THREADPOOL \_ 死锁 \_ LIVEDUMP bug 检查的值为0x000001C5。 这表示内核模式 threadpool 遇到死锁情况。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="io_threadpool_deadlock_livedump-parameters"></a>IO \_ THREADPOOL \_ 死锁 \_ LIVEDUMP 参数


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
<td align="left"><p>池号。</p>
<p>0x0： ExPoolUntrusted</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">指向 PEX_WORK_QUEUE 的指针</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">预留</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">预留</td>
</tr>
</tbody>
</table>

 

 

 




