---
title: Bug 检查 0x2B PANIC_STACK_SWITCH
description: PANIC_STACK_SWITCH bug 检查的值为0x0000002B。 这表示内核模式堆栈溢出。
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
ms.openlocfilehash: 7f72d552417809635692772e693f50341a73aecc
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534822"
---
# <a name="bug-check-0x2b-panic_stack_switch"></a>Bug 检查0x2B：紧急 \_ 堆栈 \_ 切换


紧急 \_ 情况堆栈 \_ 开关 bug 检查的值为0x0000002B。 这表示内核模式堆栈溢出。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="panic_stack_switch-parameters"></a>紧急 \_ 堆栈 \_ 开关参数


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
<td align="left"><p>捕获帧</p></td>
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

当内核模式驱动程序使用太多堆栈空间时，通常会出现此错误。 当内核中出现严重的数据损坏时，也会出现这种情况。


## <a name="resolution"></a>解决方法
[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
 

 




