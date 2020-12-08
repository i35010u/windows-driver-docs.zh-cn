---
title: 禁用内核堆栈分页
description: 禁用内核堆栈分页
keywords:
- '禁用 (全局标志的内核堆栈的分页) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac068211bc0711f90d2d68fe33b7df5e6003a442
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826159"
---
# <a name="disable-paging-of-kernel-stacks"></a>禁用内核堆栈分页


## <span id="ddk_disable_paging_of_kernel_stacks_dtools"></span><span id="DDK_DISABLE_PAGING_OF_KERNEL_STACKS_DTOOLS"></span>


**禁用内核堆栈** 标志的分页可防止非活动线程的内核模式堆栈分页。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>dps</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x80000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_DISABLE_PAGE_KERNEL_STACKS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围内的注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

通常，无法分页内核模式堆栈;保证它驻留在内存中。 但是，Windows 偶尔会对非活动线程的内核堆栈进行分页。 此标志可防止出现这种情况。

仅当线程的堆栈在物理内存中时，内核调试器才能提供有关该线程的信息。 当调试死锁时，或在其他情况下必须跟踪每个线程时，此标志尤其重要。

 

 





