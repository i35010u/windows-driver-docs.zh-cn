---
title: Bug 检查 0x30 SET_OF_INVALID_CONTEXT
description: SET_OF_INVALID_CONTEXT bug 检查具有 0x00000030 值。 这表示在陷阱帧的堆栈指针具有无效值。
ms.assetid: 77e86390-e387-4ffd-96dd-c32a98939c3a
keywords:
- Bug 检查 0x30 SET_OF_INVALID_CONTEXT
- SET_OF_INVALID_CONTEXT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SET_OF_INVALID_CONTEXT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c7d4e9479bd54d359a1fd1c59115cd95159dde72
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568098"
---
# <a name="bug-check-0x30-setofinvalidcontext"></a>Bug 检查 0x30：设置\_OF\_无效\_上下文


在集中\_OF\_无效\_上下文错误检查的值为 0x00000030。 这表示在陷阱帧的堆栈指针具有无效值。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="setofinvalidcontext-parameters"></a>设置\_OF\_无效\_上下文参数


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
<td align="left"><p>新的堆栈指针</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>旧的堆栈指针</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>陷阱帧地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

一些例程尝试以较低的值与当前的堆栈指针值在陷阱帧中设置的堆栈指针时，将出现此 bug 检查。

如果没有已捕获此错误，它会导致内核以运行与指向不再有效的堆栈的堆栈指针。

 

 




