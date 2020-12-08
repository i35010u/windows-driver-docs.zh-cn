---
title: C28141
description: 警告 C28141 参数会导致 IRQ 级别设置为低于当前 IRQL，因此不能将此函数用于此目的。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28141
ms.openlocfilehash: a06627bb8905e6737d27b6b6d379856350ba2ee8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793203"
---
# <a name="c28141"></a>C28141


警告 C28141：参数将导致 IRQ 级别设置为低于当前 IRQL，因此此函数无法用于该目的

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>&lt; <em>IRQL</em> &gt; 在行 &lt; <em>行号</em> &gt; "上，irql 上次设置为 irql</p></td>
</tr>
</tbody>
</table>

 

降低调用方正在执行的 IRQL 的函数调用被不当使用。 通常，函数调用会将 IRQL 降低为更常规例程的一部分，或旨在引发调用方的 IRQL。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例 elicits 此警告。

```
KeRaiseIrql(DISPATCH_LEVEL, &OldIrql);
KeRaiseIrql(PASSIVE_LEVEL, &OldIrql);
```

下面的代码示例可避免此警告。

```
KeRaiseIrql(DISPATCH_LEVEL, &OldIrql);
KeLowerIrql(OldIrql);
```

 

 





