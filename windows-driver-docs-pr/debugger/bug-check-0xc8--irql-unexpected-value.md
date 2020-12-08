---
title: Bug 检查 0xC8 IRQL_UNEXPECTED_VALUE
description: IRQL_UNEXPECTED_VALUE bug 检查的值为0x000000C8。 这表明该处理器的 IRQL 目前并不应如此。
keywords:
- Bug 检查 0xC8 IRQL_UNEXPECTED_VALUE
- IRQL_UNEXPECTED_VALUE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IRQL_UNEXPECTED_VALUE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 00d0def668079ee8b7e02069a2df0fa8aca6cfe2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841157"
---
# <a name="bug-check-0xc8-irql_unexpected_value"></a>Bug 检查0xC8： IRQL \_ 意外 \_ 值


IRQL \_ 意外 \_ 值 bug 检查的值为0x000000C8。 这表明该处理器的 IRQL 目前并不应如此。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="irql_unexpected_value-parameters"></a>IRQL \_ 意外 \_ 值参数


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
<td align="left"><p>以下位计算的值：</p>
<p> (当前 IRQL &lt; &lt; 16) | (预期的 irql &lt; &lt; 8) |UniqueValue</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>零或 <strong>APC- &gt; KernelRoutine</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>零或 <strong>APC</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>零或 <strong>APC- &gt; NormalRoutine</strong></p></td>
</tr>
</tbody>
</table>

 

可以通过计算 (参数1和 0xFF) 来确定 "UniqueValue"。 如果 "UniqueValue" 为零或1，参数2、参数3和参数4将等于指示的 APC 指针。 否则，这些参数将等于零。

<a name="cause"></a>原因
-----

此错误通常是由设备驱动程序或另一个较低级别的程序导致的，这些程序在某段时间内更改了 IRQL，而在该时间段结束时未还原原始的 IRQL。 例如，例程可能已获取旋转锁，但未能释放它。

 

 




