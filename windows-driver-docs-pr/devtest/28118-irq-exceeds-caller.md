---
title: C28118
description: irq-exceeds-caller
ms.assetid: ''
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28118
ms.openlocfilehash: cbd3d7b47e1ec7c78d78b8f974d55d4e47551329
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361446"
---
# <a name="c28118"></a>C28118

警告：C28118:复制整个 IRP 堆栈条目离开初始化，应清除或更新某些字段。

当前函数允许在上面的 %func%（级别 %%） 允许的最大的 IRQ 级别运行。 以前的函数调用或批注不一致并使用该函数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>当前功能时，可能需要<em>IRQL_requires_max</em>，也可能是由一些以前调用设置的限制。</p></td>
</tr>
</tbody>
</table>

要调用的函数仅限于或以下某些 IRQL 被调用。  调用 （当前） 函数允许在某些更高版本的 IRQL 运行，进行该调用会导致被调用的函数，它不能在运行的 IRQL 在运行。

请注意，PREfast 将尝试推断其有关当前 IRQ 级别，可以仅当它具有推断充足信息来检测错误的 IRQ 级别时，会生成此警告。  推理可能来自所分析函数的签名或在当前路径上的之前调用。
