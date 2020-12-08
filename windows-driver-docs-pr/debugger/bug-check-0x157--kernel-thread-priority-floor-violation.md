---
title: Bug 检查 0x157 KERNEL_THREAD_PRIORITY_FLOOR_VIOLATION
description: ATTEMPTED_SWITCH_FROM_DPC bug 检查的值为0x00000157。 这表示在特定线程的优先级楼层上尝试了非法操作。
keywords:
- Bug 检查 0x157 KERNEL_THREAD_PRIORITY_FLOOR_VIOLATION
- KERNEL_THREAD_PRIORITY_FLOOR_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_THREAD_PRIORITY_FLOOR_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2079ba6d68139f17c4e23431ab5ee8f62f470e94
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820969"
---
# <a name="bug-check-0x157-kernel_thread_priority_floor_violation"></a>Bug 检查0x157：内核 \_ 线程 \_ 优先级 \_ 底价 \_ 违规


\_ \_ 从 DPC BUG 检查尝试的开关的 \_ 值为0x00000157。 这表示在特定线程的优先级楼层上尝试了非法操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="kernel_thread_priority_floor_violation-parameters"></a>内核 \_ 线程 \_ 优先级 \_ 底价 \_ 违规参数


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
<td align="left">目标优先级值</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left"><p>指示违规性质的状态代码</p>
0x1：目标优先级的优先级计数器超出流的0x2：目标优先级下的优先级计数器-流动的0x3：目标优先级值是非法的</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">预留</td>
</tr>
</tbody>
</table>

 

 

 




