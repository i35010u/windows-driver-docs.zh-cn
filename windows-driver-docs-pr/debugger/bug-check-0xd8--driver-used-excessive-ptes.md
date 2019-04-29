---
title: Bug 检查 0xD8 DRIVER_USED_EXCESSIVE_PTES
description: DRIVER_USED_EXCESSIVE_PTES bug 检查具有 0x000000D8 值。 这表示，有没有更多的系统页表项 (PTE) 剩余。
ms.assetid: a11212eb-8dd7-49f3-9b23-237ed88b9cff
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
ms.openlocfilehash: 14a782223f3bcd1842ca9cc06f6f6d103c60be49
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371741"
---
# <a name="bug-check-0xd8-driverusedexcessiveptes"></a>Bug 检查 0xD8：驱动程序\_USED\_过量\_PTE


该驱动程序\_USED\_过量\_PTE bug 检查的值为 0x000000D8。 这表示，有没有更多的系统页表项 (PTE) 剩余。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="driverusedexcessiveptes-parameters"></a>驱动程序\_USED\_过量\_PTE 参数


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
<td align="left"><p>为导致错误 （Unicode 字符串） 的驱动程序的名称的指针或为零</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>Pte 驱动程序导致了错误 （如果参数 1 为非零值） 使用数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>总可用的系统 Pte</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>总系统 Pte</p></td>
</tr>
</tbody>
</table>

 

如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) **KiBugCheckDriver**。

<a name="cause"></a>原因
-----

这通常被由于不正确地清理其内存使用的驱动程序。 参数 1 显示了占用了大多数 Pte 驱动程序。 调用堆栈会显示哪个驱动程序实际上导致 bug 检查。

<a name="resolution"></a>分辨率
----------

这两个驱动程序可能需要修复。 系统 Pte 总数可能还需要增加。

 

 




