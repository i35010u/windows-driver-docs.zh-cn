---
title: Bug 检查 0xFC ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
description: ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY bug 检查的值为0x000000FC。 这表示尝试执行不可执行的内存。
ms.assetid: bece76bd-03ca-40fd-a69b-f6cc05d09806
keywords:
- Bug 检查 0xFC ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
- ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d50724bba4a07e9c181100a55bba8f08df34bc34
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534784"
---
# <a name="bug-check-0xfc-attempted_execute_of_noexecute_memory"></a>Bug 检查0xFC：尝试 \_ 执行 \_ \_ NOEXECUTE \_ 内存


尝试 \_ 执行 \_ 的 \_ NOEXECUTE \_ 内存 bug 检查的值为0x000000FC。 这表示尝试执行不可执行的内存。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="attempted_execute_of_noexecute_memory-parameters"></a>已 \_ 尝试 \_ 执行 \_ NOEXECUTE \_ 内存参数


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
<td align="left"><p>尝试执行的虚拟地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>页表项的内容（PTE）</p></td>
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

 

<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
如果可能，尝试执行不可执行的内存的驱动程序名称的 Unicode 字符串将打印在 bug 检查屏幕上，也保存在**KiBugCheckDriver**中。 否则，通常可以通过运行堆栈跟踪，然后查看当前指令指针来找到相关驱动程序。

 

 




