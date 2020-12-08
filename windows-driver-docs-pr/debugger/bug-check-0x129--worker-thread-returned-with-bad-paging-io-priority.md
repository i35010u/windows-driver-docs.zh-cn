---
title: Bug 检查 0x129 WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY
description: WORKER_THREAD_RETURNED_WITH_BAD_PAGING_IO_PRIORITY bug 检查的值为0x00000129，表示 IOPriority 错误地修改了工作线程。
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
ms.openlocfilehash: 70667633053b3d89792b935036b0f5b435971986
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832533"
---
# <a name="bug-check-0x129-worker_thread_returned_with_bad_paging_io_priority"></a>Bug 检查0x129： \_ \_ 返回 \_ 了 \_ 错误 \_ 分页 \_ IO \_ 优先级的工作线程


\_ \_ \_ 使用 \_ 错误 \_ 分页 \_ IO 优先级 bug 检查返回的工作线程的 \_ 值为0x00000129。 这表示调用的辅助角色 IOPriority 错误地修改了工作线程分页。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="worker_thread_returned_with_bad_paging_io_priority-parameters"></a>\_ \_ 返回 \_ 了 \_ 错误 \_ 分页 \_ IO \_ 优先级参数的工作线程


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
<td align="left"><p>辅助角色例程的地址</p>
<p>使用 ln (列出此地址上的 <strong><a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">最接近符号) </a></strong> 命令查找有问题的驱动程序。</p></td>
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

 

 

 




