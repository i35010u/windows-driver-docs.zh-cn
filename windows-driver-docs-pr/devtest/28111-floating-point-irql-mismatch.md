---
title: C28111
description: 保存浮点状态警告 C28111 IRQL 与当前 IRQL （适用于此恢复操作） 不匹配。
ms.assetid: 3573ebf0-5f5b-4b04-835a-7dba36e95e8c
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28111
ms.openlocfilehash: 1cc2af385b96e1177fce0c8e425eab5c19fcf1bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576302"
---
# <a name="c28111"></a>C28111


警告 C28111:保存浮点状态的 IRQL 与当前 IRQL （适用于此恢复操作） 不匹配。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>浮动的保存/还原功能要求 IRQL 相同在保存的时间和相应的还原。</p></td>
</tr>
</tbody>
</table>

 

还原浮点状态时执行该驱动程序 IRQL 与不同的执行时保存浮点状态的 IRQL。

驱动程序在运行的 IRQL 确定如何保存浮点状态，因为驱动程序必须执行相同的 IRQL 在中，当调用函数以保存并还原浮点状态。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

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

 

 





