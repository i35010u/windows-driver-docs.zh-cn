---
title: Bug 检查 0xE1 WORKER_THREAD_RETURNED_AT_BAD_IRQL
description: WORKER_THREAD_RETURNED_AT_BAD_IRQL bug 检查具有 0x000000E1 值。 这表示一个工作线程完成并返回与 IRQL DISPATCH_LEVEL。
ms.assetid: c02b98e9-e3a4-473a-bd9f-3130b7e58c1d
keywords:
- Bug 检查 0xE1 WORKER_THREAD_RETURNED_AT_BAD_IRQL
- WORKER_THREAD_RETURNED_AT_BAD_IRQL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_AT_BAD_IRQL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 63c6a16001068a9eecb9ebd48260f728d4680f9a
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238329"
---
# <a name="bug-check-0xe1-workerthreadreturnedatbadirql"></a>Bug 检查 0xE1：辅助角色\_线程\_返回\_处\_错误\_IRQL


辅助角色\_线程\_返回\_处\_错误\_IRQL bug 检查的值为 0x000000E1。 这表示一个工作线程完成并返回与 IRQL &gt;= 调度\_级别。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="workerthreadreturnedatbadirql-parameters"></a>辅助角色\_线程\_返回\_处\_错误\_IRQL 参数


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
<td align="left"><p>工作线程例程的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>在返回工作线程的 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>工作项的参数</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>工作项的地址</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

一个工作线程完成并返回与 IRQL &gt;= 调度\_级别。

<a name="resolution"></a>分辨率
----------

若要查找驱动程序导致了错误，请使用[ **ln （列表最接近符号）** ](ln--list-nearest-symbols-.md)调试器命令：

```dbgcmd
kd> ln address
```

其中*地址*是参数 1 中给定的辅助角色例程地址。

 

 




