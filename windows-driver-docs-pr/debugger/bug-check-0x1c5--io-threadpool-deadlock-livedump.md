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
ms.openlocfilehash: 60dec231d7b4f741f72dc0cfba0f0b9080702f83
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519723"
---
# <a name="bug-check-0x1c5-iothreadpooldeadlocklivedump"></a>Bug 检查 0x1C5：IO\_THREADPOOL\_死锁\_LIVEDUMP


IO\_THREADPOOL\_死锁\_LIVEDUMP bug 检查的值为 0x000001C5。 这表示内核模式线程池遇到死锁情况。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


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

 

 

 




