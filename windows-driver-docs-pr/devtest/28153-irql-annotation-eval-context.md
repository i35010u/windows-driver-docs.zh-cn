---
title: C28153
description: 警告的 C28153 无法在此上下文中计算 IRQL 从批注的值。
ms.assetid: 384d0925-b23b-4ba7-b5fb-34bb7106ca3f
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28153
ms.openlocfilehash: d7ce1480a9e51784b791044a69f54e3a0a015b7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361355"
---
# <a name="c28153"></a>C28153


警告 C28153:无法在此上下文中计算 IRQL 从批注的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>可能的批注时出错。</p>
<p>以下计算： &lt; <em>val</em>&gt;</p></td>
</tr>
</tbody>
</table>

 

此警告意味着代码分析工具不能解释函数批注，因为该批注不正确编码。 因此，代码分析工具无法确定指定的 IRQL 值。

此警告可能会出现任何提及 IRQL 时无法计算表达式的 IRQL，代码分析工具的特定于驱动程序的批注。

 

 





