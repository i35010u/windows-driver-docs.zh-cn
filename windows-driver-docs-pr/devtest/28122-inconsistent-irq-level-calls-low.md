---
title: C28122
description: 警告 C28122 函数不允许在较低的 IRQ 级别调用。 以前的函数调用是与此约束不一致。
ms.assetid: 4bc2f85e-055c-4821-9260-a223be787daf
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28122
ms.openlocfilehash: a389313c6c9a794ba516c288dd9ceb9e077855ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361433"
---
# <a name="c28122"></a>C28122


警告 C28122:不允许在较低的 IRQ 级别调用该函数。 以前的函数调用是与此约束不一致。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>上次设置最大的法律 IRQL &lt; <em>IRQL</em> &gt;行&lt;<em>行号</em>&gt;。 可能会错误实际上是一些范围有限的先前调用中。</p></td>
</tr>
</tbody>
</table>

 

驱动程序执行过低，不足以它所调用的函数的 IRQL 在和中的当前函数之前调用最高允许 IRQL 低于最小的 IRQL 所需的此调用。

当代码分析工具将报告此警告时，参考 WDK 文档以了解函数序列，并验证每个函数可调用的 IRQL。

代码分析工具推断当前 IRQL，并且仅当其已推断足够有关 IRQL 来检测错误时将报告此警告。 可能会根据此推断*函数签名*（参数和结果类型） 所分析函数或从先前调用的执行路径中。

类似的情况的说明，请参阅[警告 28123](28123-inconsistent-irq-level-calls-high.md)。

 

 





