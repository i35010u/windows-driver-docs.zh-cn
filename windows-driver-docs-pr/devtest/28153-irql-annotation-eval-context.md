---
title: C28153
description: 警告 C28153 在此上下文中无法计算来自批注的 IRQL 值。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28153
ms.openlocfilehash: c77e93602575a6bc3b80da30918877c49b471bae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793166"
---
# <a name="c28153"></a>C28153


警告 C28153：在此上下文中无法计算来自批注的 IRQL 值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>可能的批注错误。</p>
<p>已计算以下内容： &lt; <em>val</em>&gt;</p></td>
</tr>
</tbody>
</table>

 

此警告意味着代码分析工具无法解释函数注释，因为批注未正确编码。 因此，代码分析工具无法确定指定的 IRQL 值。

当代码分析工具无法对 IRQL 的表达式求值时，如果出现任何特定于驱动程序的批注，则会出现此警告。

 

 





