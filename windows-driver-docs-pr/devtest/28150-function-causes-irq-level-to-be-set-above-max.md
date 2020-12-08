---
title: C28150
description: 警告 C28150 此函数会导致 IRQ 级别设置为高于要分析的函数的最大可接受值。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28150
ms.openlocfilehash: 1d6b85982ddb058bfb8a25d51c07aa90d1f0d720
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793171"
---
# <a name="c28150"></a>C28150


警告 C28150：该函数导致 IRQ 级别设置为高于要分析的函数的最大可接受值

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>级别限制来自当前函数的注释。</p></td>
</tr>
</tbody>
</table>

 

指定函数在当前函数调用所允许的最大 IRQL 以上引发了 IRQL。

此警告出现在已使用 **\_ \_ winspool.drv \_ maxIRQL** 批注批注的函数中，并且指示函数中的编码错误或批注中函数协定的误解。

 

 





