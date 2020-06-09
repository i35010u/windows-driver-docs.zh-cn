---
title: Bug 检查 0xFF RESERVE_QUEUE_OVERFLOW
description: RESERVE_QUEUE_OVERFLOW bug 检查的值为0x000000FF。 这表示尝试将新项插入保留队列，导致队列溢出。
ms.assetid: d327ea41-c568-49f6-8b37-183533fd6261
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
ms.openlocfilehash: 898e2e8608fe40bc455fffc32d10c6e671e05156
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534506"
---
# <a name="bug-check-0xff-reserve_queue_overflow"></a>Bug 检查0xFF：保留 \_ 队列 \_ 溢出


保留 \_ 队列 \_ 溢出 bug 检查的值为0x000000FF。 这表示尝试将新项插入保留队列，导致队列溢出。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="reserve_queue_overflow-parameters"></a>保留 \_ 队列 \_ 溢出参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
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
 

 




