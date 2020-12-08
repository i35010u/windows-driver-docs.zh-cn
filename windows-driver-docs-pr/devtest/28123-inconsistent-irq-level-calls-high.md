---
title: C28123
description: 警告 C28123 不允许在高 IRQ 级别调用此函数。 以前的函数调用与此约束不一致。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28123
ms.openlocfilehash: 25333b385432c9ebd1edced04422e58a415e9526
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829957"
---
# <a name="c28123"></a>C28123


警告 C28123：不允许在高 IRQ 级别调用此函数。 以前的函数调用与此约束不一致。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>这可能是因为此错误实际上是某些以前的调用限制范围。</p></td>
</tr>
</tbody>
</table>

 

该驱动程序在其所调用的函数的值太高，并且函数内之前调用的最小允许 IRQL 大于此调用所需的最大 IRQL。

当代码分析工具报告此警告时，请查看函数序列的 WDK 文档，并验证可调用每个函数的 IRQL。

代码分析工具将推断当前的 IRQL，并仅当它已推断出足够多的 IRQL 来检测错误时才报告此警告。 此推理可能基于 *函数签名* (要分析的函数的参数和结果类型) ，或从执行路径中的先前调用开始。

 

 





