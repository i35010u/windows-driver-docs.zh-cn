---
title: Bug 检查 0xDF IMPERSONATING_WORKER_THREAD
description: IMPERSONATING_WORKER_THREAD bug 检查具有 0x000000DF 值。 这表示一个工作项未完成之前禁用模拟。
ms.assetid: d8a68b5b-3aa8-4d02-8063-420834a47f1b
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
ms.openlocfilehash: 451058389cdf553c7cd55e3722c36b18f1209ce6
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238406"
---
# <a name="bug-check-0xdf-impersonatingworkerthread"></a>Bug 检查 0xDF：模拟\_辅助\_线程


正在模拟\_辅助\_线程 bug 检查的值为 0x000000DF。 这表示一个工作项未完成之前禁用模拟。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="impersonatingworkerthread-parameters"></a>模拟\_辅助\_线程参数


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
<td align="left"><p>导致此错误的辅助角色例程</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>传递给此工作线程例程的参数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>指向工作项的指针</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

一个工作线程正在模拟另一个进程，并禁用然后再返回模拟失败。

 

 




