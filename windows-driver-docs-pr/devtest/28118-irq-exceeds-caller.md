---
title: C28118
description: irq-超过-调用方
ms.assetid: ''
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28118
ms.openlocfilehash: 8e92343225daba43c7d38bbe29d77e56cb37f61b
ms.sourcegitcommit: 4a3e5c2c6f9d1b6ea03e81e4da641a48122b2307
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2019
ms.locfileid: "70014871"
---
# <a name="c28118"></a>C28118

出现C28118:允许当前函数在 IRQ 级别运行, 超过% func% (% level%) 允许的最大值。 以前的函数调用或批注不一致, 不能使用该函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>附加信息</strong></p></td>
<td align="left"><p>当前函数可能需要<em>IRQL_requires_max</em>, 也可能是由某些先前调用设置的限制。</p></td>
</tr>
</tbody>
</table>

被调用的函数限制为在某些 IRQL 下调用。  允许调用 (当前) 函数在一些更高的 IRQL 下运行, 并且进行该调用可能会导致调用的函数在其无法运行的 IRQL 下运行。

请注意, PREfast 将尝试推断出当前 IRQ 级别的相关信息, 并且仅当它已推断出足够的 IRQ 级别来检测错误时, 才会生成此警告。  推理可能来自正在分析的函数的签名或当前路径中的之前调用。
