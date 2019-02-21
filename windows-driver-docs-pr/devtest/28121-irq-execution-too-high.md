---
title: C28121
description: 警告 C28121 函数不允许在当前 IRQ 级别调用。 当前级别过高。
ms.assetid: f0ab65ee-e160-4118-b001-7a8ba83d9671
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28121
ms.openlocfilehash: 8c7ad92e21834e7083174855d94f8308a580c44c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521578"
---
# <a name="c28121"></a>C28121


警告 C28121:不允许在当前 IRQ 级别调用该函数。 当前级别过高。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>上次设 IRQL &lt; <em>IRQL</em> &gt;行&lt;<em>行号</em>&gt;。从函数签名中，可能已推断级别。</p></td>
</tr>
</tbody>
</table>

 

在它所调用函数过高的 IRQL 执行驱动程序。

当代码分析工具报告此警告时，请查阅函数的 WDK 文档，并验证该函数可以调用的 IRQL。

代码分析工具推断当前 IRQL，并且仅当其已推断足够有关 IRQL 来检测错误时将报告此警告。 可能会根据此推断*函数签名*（参数和结果类型） 所分析函数或从当前路径上的之前调用。

如果代码分析工具无法确定驱动程序正在的 IRQL，它不会报告此警告，即使在错误的 IRQL 调用该函数。

 

 





