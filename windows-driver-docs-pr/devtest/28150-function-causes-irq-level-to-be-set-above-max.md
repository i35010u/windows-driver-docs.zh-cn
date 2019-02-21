---
title: C28150
description: 警告 C28150 函数导致 IRQ 级别的设置高于最大值为所分析函数可接受。
ms.assetid: 7ad53801-fa7f-49c1-a1f0-715c9f4951d1
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28150
ms.openlocfilehash: d1ff92b9b831a75c62a5422b823f7bc91fce19b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525956"
---
# <a name="c28150"></a>C28150


警告 C28150:该函数导致 IRQ 级别设置高于最大值为所分析函数可接受

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>级别限制来自当前函数的批注。</p></td>
</tr>
</tbody>
</table>

 

指定的函数引发了上面的 IRQL 允许当前函数调用花费的最大 IRQL。

在已批注与函数内会出现此警告 **\_ \_drv\_maxIRQL**批注和指示该函数中的编码错误或误解在批注中的函数的协定。

 

 





