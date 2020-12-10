---
title: Bug 检查 0xC8 IRQL_UNEXPECTED_VALUE
description: IRQL_UNEXPECTED_VALUE bug 检查的值为0x000000C8。 这表明该处理器的 IRQL 目前并不应如此。
keywords:
- Bug 检查 0xC8 IRQL_UNEXPECTED_VALUE
- IRQL_UNEXPECTED_VALUE
ms.date: 12/07/2020
topic_type:
- apiref
api_name:
- IRQL_UNEXPECTED_VALUE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a857b7b5da01ff9fdde10622bf8a4070a86cc563
ms.sourcegitcommit: 11a82f18ee7874537597792cb77f749d5ce6eee5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96999149"
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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>以下位计算的值：</p>
<p> (当前 IRQL &lt; &lt; 16) | (预期的 irql &lt; &lt; 8) |UniqueValue</p></td>
</tr>
<tr class="even">
<td align="left"><p>2-依赖于 UniqueValue</p></td>
<td align="left">
<p>如果 UniqueValue 为0或1： APC >KernelRoutine。</p>
<p>如果 UniqueValue 为2：标注例程</p>
<p>如果 UniqueValue 为3：中断的 ServiceRoutine</p>
<p>如果 UniqueValue 为0xfe：如果禁用 Apc，则为1</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>3-依赖于 UniqueValue </p></td>
<td align="left">
<p>如果 UniqueValue 为0或1： APC</p>
<p>如果 UniqueValue 为2：标注的参数</p>
<p>如果 UniqueValue 为3： KINTERRUPT</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>4-依赖于 UniqueValue</p></td>
<td align="left">
<p>如果 UniqueValue 为0或1： APC >NormalRoutine</p>
</td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

此错误通常是由设备驱动程序或另一个较低级别的程序导致的，这些程序在某段时间内更改了 IRQL，而在该时间段结束时未还原原始的 IRQL。 例如，例程可能已获取旋转锁，但未能释放它。

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，并且在确定根本原因时可能非常有用。

## <a name="see-also"></a>另请参阅

[使用 Windows 调试器 (WinDbg) 进行故障转储分析](crash-dump-files.md)

[使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)
