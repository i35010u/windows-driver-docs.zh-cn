---
title: C28118
description: irq-超过-调用方
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28118
ms.openlocfilehash: 1da1e0a7079f643d685533a8c654c0094de08e88
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837815"
---
# <a name="c28118"></a>C28118

警告： C28118：允许当前函数在 IRQ 级别运行，超过% func% (% level% ) 所允许的最大值。 以前的函数调用或批注不一致，不能使用该函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>当前函数可能需要 <em>IRQL_requires_max</em>，或者它可能是由某些先前调用设置的限制。</p></td>
</tr>
</tbody>
</table>

被调用的函数限制为在某些 IRQL 下调用。  允许调用 (当前) 函数的更高的 IRQL，并使该调用可能导致调用的函数在其无法操作的 IRQL 下运行。

请注意，PREfast 将尝试推断出当前 IRQ 级别的相关信息，并且仅当它已推断出足够的 IRQ 级别来检测错误时，才会生成此警告。  推理可能来自正在分析的函数的签名或当前路径中的之前调用。
