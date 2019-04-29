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
ms.openlocfilehash: b66bc9b71a740a3bf096790db9c6ebf35a44e988
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361386"
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
<td align="left"><p>上次设 IRQL &lt; <em>IRQL</em> &gt;行&lt;<em>行号</em>&gt;"</p></td>
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

 

 





