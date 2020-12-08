---
title: Bug 检查 0xFF RESERVE_QUEUE_OVERFLOW
description: RESERVE_QUEUE_OVERFLOW bug 检查的值为0x000000FF。 这表示尝试将新项插入保留队列，导致队列溢出。
keywords:
- Bug 检查 0xFF RESERVE_QUEUE_OVERFLOW
- RESERVE_QUEUE_OVERFLOW
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RESERVE_QUEUE_OVERFLOW
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff08b52be692f2937c6c36f597a0264f1902d371
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827349"
---
# <a name="bug-check-0xff-reserve_queue_overflow"></a>Bug 检查0xFF：保留 \_ 队列 \_ 溢出


保留 \_ 队列 \_ 溢出 bug 检查的值为0x000000FF。 这表示尝试将新项插入保留队列，导致队列溢出。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="reserve_queue_overflow-parameters"></a>保留 \_ 队列 \_ 溢出参数


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
<td align="left"><p>保留队列的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留队列的大小</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

## <a name="resolution"></a>解决方法 
[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，并且在确定根本原因时可能非常有用。
 

 




