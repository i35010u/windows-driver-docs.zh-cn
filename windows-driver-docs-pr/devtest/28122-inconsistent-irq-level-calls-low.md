---
title: C28122
description: 警告 C28122 不允许在较低的 IRQ 级别调用该函数。 以前的函数调用与此约束不一致。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28122
ms.openlocfilehash: d6d1e832f1a237a056f042f17bb5a7ea7417658d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840199"
---
# <a name="c28122"></a>C28122


警告 C28122：不允许在较低的 IRQ 级别调用该函数。 以前的函数调用与此约束不一致。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>最大合法的 &lt; <em>IRQL</em> &gt; 每个值在行 &lt; <em>号</em>处设置为 irql &gt; 。 这可能是因为此错误实际上是某些以前的调用限制范围。</p></td>
</tr>
</tbody>
</table>

 

驱动程序在其正在调用的函数的值太低的值上执行，并且当前函数中先前调用所允许的最高 IRQL 低于此调用所需的最小 IRQL。

当代码分析工具报告此警告时，请查看函数序列的 WDK 文档，并验证可调用每个函数的 IRQL。

代码分析工具将推断当前的 IRQL，并仅当它已推断出足够多的 IRQL 来检测错误时才报告此警告。 此推理可能基于 *函数签名* (要分析的函数的参数和结果类型) ，或从执行路径中的先前调用开始。

有关类似情况的说明，请参阅[警告 28123](28123-inconsistent-irq-level-calls-high.md)。

 

 





