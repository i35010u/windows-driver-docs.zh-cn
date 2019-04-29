---
title: Bug 检查 0x129 WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY
description: WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY bug 检查具有值，该值指示 0x00000129 错误地修改分页 IOPriority 工作线程。
ms.assetid: E662D301-6B4D-4E92-BED3-4BB0731DBFD0
keywords:
- Bug 检查 0x129 WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY
- WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c357bdf19c4a98dc537f53db349c8b66c7cf9c57
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354844"
---
# <a name="bug-check-0x129-workerthreadreturnedwithbadpagingiopriority"></a>Bug 检查 0x129：辅助角色\_线程\_返回\_WITH\_错误\_分页\_IO\_优先级


辅助角色\_线程\_返回\_WITH\_错误\_分页\_IO\_优先级 bug 检查的值为 0x00000129。 这指示工作线程分页 IOPriority 已错误地修改由被调用的辅助角色例程。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="workerthreadreturnedwithbadpagingiopriority-parameters"></a>辅助角色\_线程\_返回\_WITH\_错误\_分页\_IO\_优先级参数


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
<td align="left">1</td>
<td align="left"><p>工作线程例程的地址</p>
<p>使用<strong><a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">ln （列表最接近符号）</a></strong>命令此地址来查找有问题的驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">当前分页 IoPrioirity 值</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">工作项参数</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">工作项地址</td>
</tr>
</tbody>
</table>

 

 

 




