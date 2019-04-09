---
title: Bug 检查 0xAC HAL_MEMORY_ALLOCATION
description: HAL_MEMORY_ALLOCATION bug 检查具有 0x000000AC 值。 此 bug 检查指示硬件抽象层 (HAL) 无法获取足够的内存。
ms.assetid: 816e6ab5-ccec-47fb-8618-865cb5bb6cb2
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
ms.openlocfilehash: 25ef29ebdf568a657d3ed446c9585699da2b5a8d
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238620"
---
# <a name="bug-check-0xac-halmemoryallocation"></a>Bug 检查 0xAC：HAL\_内存\_分配


HAL\_内存\_分配错误检查的值为 0x000000AC。 此 bug 检查指示硬件抽象层 (HAL) 无法获取足够的内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="halmemoryallocation-parameters"></a>HAL\_内存\_分配参数


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
<td align="left"><p>指向包含文件名称的字符串的指针</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

HAL 无法获取非分页内存池的系统的关键要求。

这些关键的内存分配进行提前在系统初始化和 HAL\_内存\_不应分配 bug 检查。 检查此错误可能表示某些其他严重错误，例如池损坏或大量消耗。

 

 




