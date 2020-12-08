---
title: Bug 检查 0x2B PANIC_STACK_SWITCH
description: PANIC_STACK_SWITCH bug 检查的值为0x0000002B。 这表示内核模式堆栈溢出。
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
ms.openlocfilehash: e468b025708defee3798f256490815be5473f57c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824689"
---
# <a name="bug-check-0x2b-panic_stack_switch"></a>Bug 检查0x2B：紧急 \_ 堆栈 \_ 切换


紧急 \_ 情况堆栈 \_ 开关 bug 检查的值为0x0000002B。 这表示内核模式堆栈溢出。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="panic_stack_switch-parameters"></a>紧急 \_ 堆栈 \_ 开关参数


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
<td align="left"><p>捕获帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>预留</p></td>
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

 

<a name="cause"></a>原因
-----

当内核模式驱动程序使用太多堆栈空间时，通常会出现此错误。 当内核中出现严重的数据损坏时，也会出现这种情况。


## <a name="resolution"></a>解决方法
[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
 

 




