---
title: Bug 检查 0xBE ATTEMPTED_WRITE_TO_READONLY_MEMORY
description: ATTEMPTED_WRITE_TO_READONLY_MEMORY bug 检查的值为0x000000BE。 如果驱动程序尝试写入只读内存段，则会发出此项。
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
ms.openlocfilehash: be0219f1be94a0355509cf84e226ecad9f5fc563
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534796"
---
# <a name="bug-check-0xbe-attempted_write_to_readonly_memory"></a>Bug 检查0xBE：尝试 \_ 写入 \_ \_ 只读 \_ 内存


尝试 \_ 写入 \_ \_ READONLY \_ 内存 bug 检查的值为0x000000BE。 如果驱动程序尝试写入只读内存段，则会发出此项。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="attempted_write_to_readonly_memory-parameters"></a>尝试 \_ 写入 \_ \_ READONLY \_ 内存参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
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
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

如果可以识别负责错误的驱动程序，则会在蓝色屏幕上打印其名称，并将其存储在内存中的位置（PUNICODE \_ 字符串） **KiBugCheckDriver**。


<a name="remarks"></a>注解
-------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
 




