---
title: Bug 检查 0xBE ATTEMPTED_WRITE_TO_READONLY_MEMORY
description: ATTEMPTED_WRITE_TO_READONLY_MEMORY bug 检查的值为0x000000BE。 如果驱动程序尝试写入只读内存段，则会发出此项。
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
ms.openlocfilehash: b868e4595e69b563ba7dfe45161e849259692ac3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783548"
---
# <a name="bug-check-0xbe-attempted_write_to_readonly_memory"></a>Bug 检查0xBE：尝试 \_ 写入 \_ \_ 只读 \_ 内存


尝试 \_ 写入 \_ \_ READONLY \_ 内存 bug 检查的值为0x000000BE。 如果驱动程序尝试写入只读内存段，则会发出此项。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="attempted_write_to_readonly_memory-parameters"></a>尝试 \_ 写入 \_ \_ READONLY \_ 内存参数


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
<td align="left"><p>尝试写入的虚拟地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>PTE 内容</p></td>
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

 

如果能够识别出导致错误的驱动程序，则其名称将打印在蓝屏上，并存储在内存中的 (PUNICODE\_STRING) KiBugCheckDriver  位置。


<a name="remarks"></a>备注
-------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
 




