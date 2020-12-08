---
title: Bug 检查 0xE4 WORKER_INVALID
description: WORKER_INVALID bug 检查的值为0x000000E4。 这通常表示不应包含执行工作项的内存包含这样的项。
keywords:
- Bug 检查 0xE4 WORKER_INVALID
- WORKER_INVALID
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_INVALID
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6e9606b24df128dd7ff843404f98ac7476a51c4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788851"
---
# <a name="bug-check-0xe4-worker_invalid"></a>Bug 检查0xE4：辅助角色 \_ 无效


辅助角色 \_ 无效 bug 检查的值为0x000000E4。 这表示不应包含执行工作项的内存包含此类项，或者当前处于活动状态的工作项已排队。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="worker_invalid-parameters"></a>辅助角色 \_ 无效参数


参数1指示代码位置。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>池块的开始</p></td>
<td align="left"><p>池块结束</p></td>
<td align="left"><p>已释放活动的辅助角色项。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>队列编号</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>活动辅助角色项已排队。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>I/o 辅助角色例程的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已释放排队 i/o 辅助角色项。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>无效对象的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>尝试使用无效的对象初始化 i/o 辅助角色项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>队列编号</p></td>
<td align="left"><p>目标为的 NUMA 节点; 如果搜索所有节点，则为-1。</p></td>
<td align="left"><p>尝试对工作项进行排队后，才能初始化工作线程。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>队列编号</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>提供的队列类型无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>队列编号</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>尝试将工作项排队，使工作项无效。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

这通常是由释放内存的驱动程序（仍包含执行工作项）引起的。

 

 




