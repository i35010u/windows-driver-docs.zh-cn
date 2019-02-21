---
title: C28124
description: 警告 C28124 对的调用会导致 IRQ 级别要低于最小值设置为所分析函数可接受。
ms.assetid: d0540a52-2252-49d5-ba03-3d026e07670a
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28124
ms.openlocfilehash: 7a6ffe1c8147d9d0bcee51cbf40c46e4166e71e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521580"
---
# <a name="c28124"></a>C28124


警告 C28124:对的调用会导致 IRQ 级别要低于最小值设置为所分析函数可接受。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>上次设置最小的法律 IRQL &lt; <em>IRQL</em> &gt;行&lt;<em>行号</em>&gt;。 级别限制来自当前函数的批注。</p></td>
</tr>
</tbody>
</table>

 

该驱动程序调用更改为小于最小的 IRQL 对当前函数类型级别的 IRQL 的函数。 代码分析工具来推断此信息从函数类型或批注。

在已批注与函数内会出现此警告 **\_ \_drv\_minIRQL**批注和指示该函数中的编码错误或误解在批注中的函数的协定。

 

 





