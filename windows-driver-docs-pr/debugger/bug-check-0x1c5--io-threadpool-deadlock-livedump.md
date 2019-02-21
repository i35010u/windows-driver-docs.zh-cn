---
title: Bug 检查 0x1C5 IO_THREADPOOL_DEADLOCK_LIVEDUMP
description: IO_THREADPOOL_DEADLOCK_LIVEDUMP bug 检查具有 0x000001C5 值。 这表示内核模式线程池遇到死锁情况。
ms.assetid: CBAB931F-E2A9-4843-9565-DC1CA3B557E6
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
ms.openlocfilehash: e31823fd67d2794ba72c8c8d7706d0606cf8f620
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544047"
---
# <a name="bug-check-0x1c5-iothreadpooldeadlocklivedump"></a>Bug 检查 0x1C5:IO\_THREADPOOL\_死锁\_LIVEDUMP


IO\_THREADPOOL\_死锁\_LIVEDUMP bug 检查的值为 0x000001C5。 这表示内核模式线程池遇到死锁情况。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="iothreadpooldeadlocklivedump-parameters"></a>IO\_THREADPOOL\_死锁\_LIVEDUMP 参数


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
<td align="left"><p>池数。</p>
<p>0x0:ExPoolUntrusted</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">指向 PEX_WORK_QUEUE</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">保留</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">保留</td>
</tr>
</tbody>
</table>

 

 

 




