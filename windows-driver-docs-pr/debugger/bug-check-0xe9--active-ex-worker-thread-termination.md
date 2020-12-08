---
title: Bug 检查 0xE9 ACTIVE_EX_WORKER_THREAD_TERMINATION
description: ACTIVE_EX_WORKER_THREAD_TERMINATION bug 检查的值为0x000000E9。 这表示正在终止活动的执行工作线程。
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
ms.openlocfilehash: 9da57c403445195e85eba4bfbfd7cc7c2611ff18
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793265"
---
# <a name="bug-check-0xe9-active_ex_worker_thread_termination"></a>Bug 检查0xE9：活动 \_ EX \_ 工作 \_ 线程 \_ 终止


活动 \_ EX \_ 工作 \_ 线程 \_ 终止 bug 检查的值为0x000000E9。 这表示正在终止活动的执行工作线程。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="active_ex_worker_thread_termination-parameters"></a>活动 \_ EX \_ 工作 \_ 线程 \_ 终止参数


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
<td align="left"><p>退出 ETHREAD</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

不通过工作线程断开代码就终止了 executive 工作线程。 禁止这种情况;排队到 **ExWorkerQueue** 的工作项不能终止其线程。

堆栈跟踪应指出原因。

 

 




