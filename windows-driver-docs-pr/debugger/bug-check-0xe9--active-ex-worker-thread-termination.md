---
title: Bug 检查 0xE9 ACTIVE_EX_WORKER_THREAD_TERMINATION
description: ACTIVE_EX_WORKER_THREAD_TERMINATION bug 检查具有 0x000000E9 值。 这表示正在终止活动执行的工作线程。
ms.assetid: dd68f07f-fab1-402c-9a81-f43722f91b69
keywords:
- Bug 检查 0xE9 ACTIVE_EX_WORKER_THREAD_TERMINATION
- ACTIVE_EX_WORKER_THREAD_TERMINATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ACTIVE_EX_WORKER_THREAD_TERMINATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f31bb9b0ede63709dfdcadd17a22f060fc00b505
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568255"
---
# <a name="bug-check-0xe9-activeexworkerthreadtermination"></a>Bug 检查 0xE9：ACTIVE\_EX\_辅助角色\_线程\_终止


活动\_EX\_辅助角色\_线程\_终止 bug 检查的值为 0x000000E9。 这表示正在终止活动执行的工作线程。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="activeexworkerthreadtermination-parameters"></a>ACTIVE\_EX\_辅助角色\_线程\_终止参数


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
<td align="left"><p>正在退出 ETHREAD</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

不具有经历的辅助线程断开代码的情况下，正在终止执行的工作线程。 这是禁止的;工作项排队**ExWorkerQueue**必须终止它们的线程。

堆栈跟踪应该指示的原因。

 

 




