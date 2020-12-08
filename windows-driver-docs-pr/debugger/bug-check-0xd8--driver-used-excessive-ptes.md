---
title: Bug 检查 0xD8 DRIVER_USED_EXCESSIVE_PTES
description: DRIVER_USED_EXCESSIVE_PTES bug 检查的值为0x000000D8。 这表明 (PTE) 剩余的系统页表项不存在。
keywords:
- Bug 检查 0xD8 DRIVER_USED_EXCESSIVE_PTES
- DRIVER_USED_EXCESSIVE_PTES
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_USED_EXCESSIVE_PTES
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b92e46bc36704bd644461b10f1791f954d05f055
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787923"
---
# <a name="bug-check-0xd8-driver_used_excessive_ptes"></a>Bug 检查0xD8：驱动程序 \_ 使用 \_ 过多 \_ pte


\_使用 \_ 过多 pte bug 检查的驱动程序的 \_ 值为0x000000D8。 这表明 (PTE) 剩余的系统页表项不存在。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="driver_used_excessive_ptes-parameters"></a>驱动程序 \_ 使用 \_ 过多 \_ pte 参数


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
<td align="left"><p>一个指针，指向导致错误的驱动程序的名称 (Unicode 字符串) 或零</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>导致错误的驱动程序所使用的 Pte 数 (if 参数1是否为非零值) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>可用系统 Pte 总数</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>系统 Pte 总数</p></td>
</tr>
</tbody>
</table>

 

如果能够识别出导致错误的驱动程序，则其名称将打印在蓝屏上，并存储在内存中的 (PUNICODE\_STRING) KiBugCheckDriver  位置。

<a name="cause"></a>原因
-----

这通常是由于驱动程序未正确清理其内存使用而导致的。 参数1显示已使用最多 Pte 的驱动程序。 调用堆栈将揭示哪个驱动程序实际导致了 bug 检查。

<a name="resolution"></a>解决方法
----------

这两个驱动程序可能需要修复。 系统 Pte 的总数可能还需要增加。

 

 




