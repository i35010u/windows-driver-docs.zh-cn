---
title: Bug 检查 0x2B PANIC_STACK_SWITCH
description: PANIC_STACK_SWITCH bug 检查具有 0x0000002B 值。 这表示内核模式堆栈已溢出。
ms.assetid: 0ab28a16-979d-4b40-812a-a31fac3f6be8
keywords:
- Bug 检查 0x2B PANIC_STACK_SWITCH
- PANIC_STACK_SWITCH
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PANIC_STACK_SWITCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1c444000ae1f760ac982cc8b3f00e109957f97a2
ms.sourcegitcommit: 78bbc162dcf6eb5816afbfa8ac546722bb98c6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56582831"
---
# <a name="bug-check-0x2b-panicstackswitch"></a>Bug 检查 0x2B：PANIC\_堆栈\_开关


PANIC\_堆栈\_交换机 bug 检查的值为 0x0000002B。 这表示内核模式堆栈已溢出。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="panicstackswitch-parameters"></a>PANIC\_堆栈\_开关参数


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
<td align="left"><p>陷阱帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
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

 

<a name="cause"></a>原因
-----

内核模式驱动程序使用太多堆栈空间，则通常会出现此错误。 它也会出现严重的数据损坏时在内核中。


## <a name="resolution"></a>分辨率
[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息和确定根本原因非常有帮助。
 

 




