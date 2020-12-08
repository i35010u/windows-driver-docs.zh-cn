---
title: C28121
description: 警告 C28121 不允许在当前 IRQ 级别调用该函数。 当前级别过高。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28121
ms.openlocfilehash: 4a6225fc6a378d1d4f9b19b11c15bc801689d834
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829955"
---
# <a name="c28121"></a>C28121


警告 C28121：不允许在当前 IRQ 级别调用该函数。 当前级别过高。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>&lt; <em>IRQL</em> &gt; 在行 &lt; <em>行号</em>上，irql 最后设置为 irql &gt; 。可能已从函数签名中推断出该级别。</p></td>
</tr>
</tbody>
</table>

 

驱动程序正在调用的函数的无效 IRQL 上执行。

当代码分析工具报告此警告时，请参考 WDK 文档中的函数，并验证可调用函数的 IRQL。

代码分析工具将推断当前的 IRQL，并仅当它已推断出足够多的 IRQL 来检测错误时才报告此警告。 此推理可能基于 *函数签名* (要分析的函数的参数和结果类型) ，或当前路径之前的调用。

如果代码分析工具无法确定驱动程序正在其上运行的 IRQL，则不会报告此警告，即使该函数是在错误的 IRQL 下调用的。

 

 





