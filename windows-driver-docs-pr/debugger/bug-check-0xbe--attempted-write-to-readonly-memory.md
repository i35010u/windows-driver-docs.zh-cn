---
title: Bug 检查 0xBE ATTEMPTED_WRITE_TO_READONLY_MEMORY
description: ATTEMPTED_WRITE_TO_READONLY_MEMORY bug 检查具有 0x000000BE 值。 这被发出一个驱动程序尝试写入只读内存段。
ms.assetid: d6247828-09ae-4071-9b4f-917af29265bc
keywords:
- Bug 检查 0xBE ATTEMPTED_WRITE_TO_READONLY_MEMORY
- ATTEMPTED_WRITE_TO_READONLY_MEMORY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ATTEMPTED_WRITE_TO_READONLY_MEMORY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 08fc66ec8d146bbc70453c210f9573fe3c265fcc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565786"
---
# <a name="bug-check-0xbe-attemptedwritetoreadonlymemory"></a>Bug 检查 0xBE：尝试\_编写\_TO\_READONLY\_内存


已尝试\_编写\_TO\_READONLY\_内存错误检查的值为 0x000000BE。 这被发出一个驱动程序尝试写入只读内存段。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="attemptedwritetoreadonlymemory-parameters"></a>尝试\_编写\_TO\_READONLY\_内存参数


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
<td align="left"><p>虚拟地址的尝试的写入</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>PTE 内容</p></td>
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

 

如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) **KiBugCheckDriver**。


<a name="remarks"></a>备注
-------

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息和确定根本原因非常有帮助。
 




