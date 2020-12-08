---
title: Bug 检查 0xAC HAL_MEMORY_ALLOCATION
description: HAL_MEMORY_ALLOCATION bug 检查的值为0x000000AC。 此 bug 检查表明硬件抽象层 (HAL) 未能获得足够的内存。
keywords:
- Bug 检查 0xAC HAL_MEMORY_ALLOCATION
- HAL_MEMORY_ALLOCATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- HAL_MEMORY_ALLOCATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa9549e6aa8ecc38b43ca7641d7d94ad4b73efc4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832859"
---
# <a name="bug-check-0xac-hal_memory_allocation"></a>Bug 检查0xAC： HAL \_ 内存 \_ 分配


HAL \_ 内存 \_ 分配 bug 检查的值为0x000000AC。 此 bug 检查表明硬件抽象层 (HAL) 未能获得足够的内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="hal_memory_allocation-parameters"></a>HAL \_ 内存 \_ 分配参数


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
<td align="left"><p>分配大小</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>指向包含文件名的字符串的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

HAL 无法获取系统严重要求的非分页内存池。

这些关键的内存分配是在系统初始化初期进行的，并且 \_ \_ 不需要 HAL 内存分配 bug 检查。 此 bug 检查可能指示一些其他严重错误，如池损坏或大规模消耗。

 

 




