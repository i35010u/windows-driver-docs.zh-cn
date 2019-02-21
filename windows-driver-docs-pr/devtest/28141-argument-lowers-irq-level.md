---
title: C28141
description: 警告 C28141 该参数导致 IRQ 级别设置低于当前 irql，因此，此函数不能用于此目的。
ms.assetid: 5cf30e4b-beef-42e0-9d1c-85418b601acb
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28141
ms.openlocfilehash: 32b2d9bffb684f05583705f454d6c2fc6ae9942b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542611"
---
# <a name="c28141"></a>C28141


警告 C28141:该参数导致 IRQ 级别设置低于当前 irql，因此，此函数不能用于此目的

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>上次设 IRQL &lt; <em>IRQL</em> &gt;行&lt;<em>行号</em>&gt;&quot;</p></td>
</tr>
</tbody>
</table>

 

降低时执行调用方 IRQL 函数调用的不恰当地使用。 通常情况下，函数调用降低 IRQL 作为更多常规例程的一部分，或用于引发调用方的 IRQL。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

```
KeRaiseIrql(DISPATCH_LEVEL, &OldIrql);
KeRaiseIrql(PASSIVE_LEVEL, &OldIrql);
```

下面的代码示例可避免此警告。

```
KeRaiseIrql(DISPATCH_LEVEL, &OldIrql);
KeLowerIrql(OldIrql);
```

 

 





