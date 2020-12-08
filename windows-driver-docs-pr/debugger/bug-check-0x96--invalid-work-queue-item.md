---
title: Bug 检查 0x96 INVALID_WORK_QUEUE_ITEM
description: INVALID_WORK_QUEUE_ITEM bug 检查的值为0x00000096。 此 bug 检查指示删除了包含 NULL 指针的队列项。
keywords:
- Bug 检查 0x96 INVALID_WORK_QUEUE_ITEM
- INVALID_WORK_QUEUE_ITEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_WORK_QUEUE_ITEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b67eb0572aca330d71bee1e824dd727d9ca7d71
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840451"
---
# <a name="bug-check-0x96-invalid_work_queue_item"></a>Bug 检查0x96： \_ 工作 \_ 队列 \_ 项无效


无效的 \_ 工作 \_ 队列 \_ 项 bug 检查的值为0x00000096。 此 bug 检查指示删除了包含 **NULL** 指针的队列项。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="invalid_work_queue_item-parameters"></a>无效的 \_ 工作 \_ 队列 \_ 项参数


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
<td align="left"><p>队列项的地址，其 <strong>flink</strong> 或 <strong>闪烁</strong> 字段为 <strong>NULL</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>正在被引用的队列的地址。 通常，此队列是一个 <strong>ExWorkerQueue</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>ExWorkerQueue</strong>数组的基址。  (此地址有助于确定所涉及的队列是否确实是 <strong>ExWorkerQueue</strong>。 如果队列是 <strong>ExWorkerQueue</strong>，则此参数的偏移将隔离队列。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>假设队列是一个 <strong>ExWorkerQueue</strong>，则此值是在工作项有效的情况下调用的辅助进程例程的地址。  (可以使用此地址来隔离滥用工作队列的驱动程序。 ) </p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

\_ \_ \_ 当 **KeRemoveQueue** 删除其 **flink** 或 **闪烁** 字段为 **NULL** 的队列项时，将发生无效的工作队列项 bug 检查。

任何队列滥用都可能导致此错误。 但通常会发生此错误，因为工作线程的工作项被滥用。

队列中的条目只能在列表中插入一次。 从队列中删除项时，其 **flink** 字段设置为 **NULL**。 然后，在第二次删除此项时，将发生此 bug 检查。

在大多数情况下，被引用的队列是 **ExWorkerQueue** (executive 辅助角色队列) 。 为了帮助识别导致错误的驱动程序，参数4显示了在此工作项有效的情况下将调用的 worker 例程的地址。 但是，如果正在引用的队列不是 **ExWorkerQueue**，则此参数不起作用。

 

 




