---
title: C28124
description: 警告 C28124 对的调用会导致 IRQ 级别设置为低于正在分析的函数可接受的最小值。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28124
ms.openlocfilehash: 540d26b5b6770657367c6958a9d1859d334b0c69
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840419"
---
# <a name="c28124"></a>C28124


警告 C28124：对的调用会导致 IRQ 级别设置为低于正在分析的函数可接受的最小值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>最小合法的 &lt; <em>IRQL</em> &gt; 每个值在行 &lt; <em>号</em>处设置为 irql &gt; 。 级别限制来自当前函数的注释。</p></td>
</tr>
</tbody>
</table>

 

驱动程序调用的函数将 IRQL 更改为小于当前函数类型的最小 IRQL 级别。 代码分析工具从函数类型或批注推断出此信息。

此警告出现在已使用 **\_ \_ winspool.drv \_ minIRQL** 批注批注的函数中，并且指示函数中的编码错误或批注中函数协定的误解。

 

 





