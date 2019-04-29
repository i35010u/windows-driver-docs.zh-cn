---
title: C28120
description: 警告 C28120 函数不允许在当前 IRQ 级别调用。 当前级别过低。
ms.assetid: a31a7c97-e27a-4a6a-a172-41d87cab236d
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28120
ms.openlocfilehash: e92d9ed3dfdb9788ab007d7cee8f2d281cd1bcb4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361435"
---
# <a name="c28120"></a>C28120


警告 C28120:不允许在当前 IRQ 级别调用该函数。 当前级别过低。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>上次设 IRQL &lt;<em>值</em>&gt;行&lt;<em>行号</em>&gt;。 从函数签名中，可能已推断级别。</p></td>
</tr>
</tbody>
</table>

 

在它所调用函数过低的 IRQL 执行驱动程序。

当代码分析工具报告此警告时，请查阅函数的 WDK 文档，并验证该函数可以调用的 IRQL。

代码分析工具推断当前 IRQL，并且仅当其已推断足够有关 IRQL 来检测错误时将报告此警告。 可能会根据此推断*函数签名*（参数和结果类型） 所分析函数或从当前路径上的之前调用。

如果代码分析工具无法确定驱动程序正在的 IRQL，它不会报告此警告，即使在错误的 IRQL 调用该函数。

类似的情况的说明，请参阅[警告 28121](28121-irq-execution-too-high.md)。

 

 





