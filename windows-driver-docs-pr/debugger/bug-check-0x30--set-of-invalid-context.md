---
title: Bug 检查 0x30 SET_OF_INVALID_CONTEXT
description: SET_OF_INVALID_CONTEXT bug 检查的值为0x00000030。 这表示陷阱帧中的堆栈指针具有无效值。
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
ms.openlocfilehash: 17943bda549d043238937722f592adb2ed44df4b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831671"
---
# <a name="bug-check-0x30-set_of_invalid_context"></a>Bug 检查0x30：一 \_ 组 \_ 无效的 \_ 上下文


一组 \_ \_ 无效的 \_ 上下文 bug 检查的值为0x00000030。 这表示陷阱帧中的堆栈指针具有无效值。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="set_of_invalid_context-parameters"></a>一 \_ 组 \_ 无效的 \_ 上下文参数


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
<td align="left"><p>新堆栈指针</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>旧堆栈指针</p></td>
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

当某个例程尝试将捕获帧中的堆栈指针设置为低于当前堆栈指针值的值时，将发生此 bug 检查。

如果未捕获到此错误，则会导致内核运行，堆栈指针指向堆栈，该堆栈将不再有效。

 

 




