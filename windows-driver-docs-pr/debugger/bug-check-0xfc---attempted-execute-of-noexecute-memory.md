---
title: Bug 检查 0xFC ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY
description: ATTEMPTED_EXECUTE_OF_NOEXECUTE_MEMORY bug 检查具有 0x000000FC 值。 这表示尝试执行不可执行的内存。
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
ms.openlocfilehash: 285f68e93c430c184c082926d368186e1cf68cac
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518701"
---
# <a name="bug-check-0xfc-attemptedexecuteofnoexecutememory"></a>Bug 检查 0xFC：尝试\_EXECUTE\_OF\_NOEXECUTE\_内存


已尝试\_EXECUTE\_OF\_NOEXECUTE\_内存错误检查的值为 0x000000FC。 这表示尝试执行不可执行的内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="attemptedexecuteofnoexecutememory-parameters"></a>尝试\_EXECUTE\_OF\_NOEXECUTE\_内存参数


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
<td align="left"><p>尝试执行的虚拟地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>页表项 (PTE) 的内容</p></td>
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

 

<a name="resolution"></a>分辨率
----------

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，有助于在确定根本原因。
如果可能，请尝试执行不可执行的内存的驱动程序名称的 Unicode 字符串 bug 检查屏幕上打印，并且也保存在**KiBugCheckDriver**。 否则，通常可以通过运行堆栈跟踪，然后查看当前指令指针找到有问题的驱动程序。

 

 




