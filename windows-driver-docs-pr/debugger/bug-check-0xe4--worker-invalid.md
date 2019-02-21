---
title: Bug 检查 0xE4 WORKER_INVALID
description: WORKER_INVALID bug 检查具有 0x000000E4 值。 这通常表明内存不应包含高级管理人员的工作项包含此类项。
ms.assetid: 93951b77-bedf-4781-9c2b-e8df2aa8cb1c
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
ms.openlocfilehash: 5e4b621d134d4086c8d511f4c1cd853f0b69b98e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554771"
---
# <a name="bug-check-0xe4-workerinvalid"></a>Bug 检查 0xE4:辅助角色\_无效


工作线程\_无效错误检查的值为 0x000000E4。 这指示该内存，不应包含一个执行的工作项包含一个项，或当前处于活动状态的工作项已排入队列。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="workerinvalid-parameters"></a>辅助角色\_无效的参数


参数 1 指示代码位置。

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
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>池块的开头</p></td>
<td align="left"><p>池块的末尾</p></td>
<td align="left"><p>活动工作项已释放。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>队列编号</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已排队的活动工作项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>I/O 工作线程例程的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已释放排队的 I/O 工作项。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>无效的对象的地址</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>尝试初始化具有无效的对象的 I/O 工作项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>队列编号</p></td>
<td align="left"><p>目标的 NUMA 节点或-1，如果所有节点的都搜索。</p></td>
<td align="left"><p>尝试将工作项排队之前初始化的工作排入队列。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>队列编号</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>提供无效的队列类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>工作项的地址</p></td>
<td align="left"><p>队列编号</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>尝试使用无效的辅助进程例程地址将工作项排队。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

这通常被由于释放内存，其中还包含一个执行的工作项的驱动程序。

 

 




