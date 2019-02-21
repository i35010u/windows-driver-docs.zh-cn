---
title: C28123
description: 警告 C28123 函数不允许在较高的 IRQ 级别调用。 以前的函数调用是与此约束不一致。
ms.assetid: 6b40a485-f4f7-4c68-8575-960faa8cb87b
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28123
ms.openlocfilehash: 65a46c21162db7e0fd3fc49cc800c3a17638732c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542710"
---
# <a name="c28123"></a>C28123


警告 C28123:不允许在较高的 IRQ 级别调用该函数。 以前的函数调用是与此约束不一致。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>可能会错误实际上是一些范围有限的先前调用中。</p></td>
</tr>
</tbody>
</table>

 

在它所调用函数过高的 IRQL 执行驱动程序和先前调用的函数中最小允许 IRQL 大于最大的 IRQL 所需的此调用。

当代码分析工具将报告此警告时，参考 WDK 文档以了解函数序列，并验证每个函数可调用的 IRQL。

代码分析工具推断当前 IRQL，并且仅当其已推断足够有关 IRQL 来检测错误时将报告此警告。 可能会根据此推断*函数签名*（参数和结果类型） 所分析函数或从先前调用的执行路径中。

 

 





