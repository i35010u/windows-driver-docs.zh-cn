---
title: Bug 检查 0xDF IMPERSONATING_WORKER_THREAD
description: IMPERSONATING_WORKER_THREAD bug 检查的值为0x000000DF。 这表明工作项未在完成之前禁用模拟。
keywords:
- Bug 检查 0xDF IMPERSONATING_WORKER_THREAD
- IMPERSONATING_WORKER_THREAD
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IMPERSONATING_WORKER_THREAD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 953a670287306e05fe5c5d6de40505ee1f0117dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787841"
---
# <a name="bug-check-0xdf-impersonating_worker_thread"></a>Bug 检查0xDF：模拟 \_ 工作 \_ 线程


模拟 \_ 工作 \_ 线程 bug 检查的值为0x000000DF。 这表明工作项未在完成之前禁用模拟。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="impersonating_worker_thread-parameters"></a>模拟 \_ 工作 \_ 线程参数


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
<td align="left"><p>导致此错误的辅助进程例程</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>传递给此辅助进程例程的参数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>指向工作项的指针</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

工作线程正在模拟其他进程，但未能在返回之前禁用模拟。

 

 




