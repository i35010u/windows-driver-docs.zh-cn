---
title: C28111
description: 警告 C28111 保存浮点状态的 IRQL 与当前 IRQL () 的此还原操作不匹配。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28111
ms.openlocfilehash: da383a2514bee6a2b2d5215af09d386fcfb36c66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838801"
---
# <a name="c28111"></a>C28111


警告 C28111：保存浮点状态的 IRQL 与当前 IRQL () 此还原操作不匹配。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>浮动保存/还原函数要求在保存时具有相同的 IRQL 和相应的还原。</p></td>
</tr>
</tbody>
</table>

 

驱动程序在还原浮点状态时执行的 IRQL 不同于它在保存浮点状态时所执行的 IRQL 操作。

由于驱动程序运行的 IRQL 决定了如何保存浮点状态，因此当驱动程序调用函数来保存和还原浮点状态时，必须在相同的 IRQL 处执行该驱动程序。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例 elicits 此警告。

```
void driver_utility()
{
    // running at APC level
    KFLOATING_SAVE FloatBuf;
    if (KeSaveFloatingPointState(&FloatBuf))
    {
        KeLowerIrql(PASSIVE_LEVEL);
        ...
        KeRestoreFloatingPointState(&FloatBuf);
    }
}
```

下面的代码示例可避免此警告。

```
void driver_utility()
{
    // running at APC level
    KFLOATING_SAVE FloatBuf;
    if (KeSaveFloatingPointState(&FloatBuf))
    {
        KeLowerIrql(PASSIVE_LEVEL);
        ...
        KeRaiseIrql(APC_LEVEL, &old);
        KeRestoreFloatingPointState(&FloatBuf);
    }
}
```

 

 





