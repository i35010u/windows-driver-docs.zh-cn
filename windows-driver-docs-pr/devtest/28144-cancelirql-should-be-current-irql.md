---
title: C28144
description: 警告 C28144 在取消例程内，在退出时，Irp 中的 IRQL-Irp->cancelirql 应为当前的 IRQL。
ms.assetid: f89a2f9b-6e84-4696-80c3-79b8760c9b4a
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28144
ms.openlocfilehash: aea3498b33b42fd564c16aa1f5c9f937ecbf1ce8
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383199"
---
# <a name="c28144"></a>C28144


警告 C28144：在退出例程内，Irp 中的 IRQL- &gt; irp->cancelirql 应为当前 irql。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>其他信息</p></td>
<td align="left"><p>此值不需要由任何特定函数还原，但必须在退出前还原。 PREfast 无法确定它是否已还原为所需的值。</p></td>
</tr>
</tbody>
</table>

 

当驱动程序的 [**Cancel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程退出时， ** &gt; irp->cancelirql** 成员的值不是当前的 IRQL。 通常情况下，当驱动程序未使用由最新的[**IoAcquireCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))调用提供的 IRQL 调用[**IoReleaseCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))时，会发生此错误。

有关 *取消* 例程的详细信息，请参阅 [取消 irp](../kernel/canceling-irps.md)。 有关特定于此警告的信息，请参阅 [取消 Irp 时要考虑的要点](../kernel/points-to-consider-when-canceling-irps.md)。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例 elicits 此警告。

```
IoReleaseCancelSpinLock(PASSIVE_LEVEL);
```

下面的代码示例可避免此警告。

```
IoReleaseCancelSpinLock(Irp->CancelIrql);
```

 

