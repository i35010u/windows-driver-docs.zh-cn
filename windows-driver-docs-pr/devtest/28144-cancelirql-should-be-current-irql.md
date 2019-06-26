---
title: C28144
description: 在取消例程，在退出时，警告 C28144 内 Irp-CancelIrql 中的 IRQL 应为当前 IRQL。
ms.assetid: f89a2f9b-6e84-4696-80c3-79b8760c9b4a
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28144
ms.openlocfilehash: e14aad810dd78a23cd49b80f571c09661c2f59d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364128"
---
# <a name="c28144"></a>C28144


警告 C28144:在取消例程，退出，在 Irp 的 IRQL&gt;CancelIrql 应为当前 IRQL。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>其他信息</strong></p></td>
<td align="left"><p>该值不需要还原的任何特定的函数，但退出之前，必须还原。 PREfast 无法确定它已还原到所需的值。</p></td>
</tr>
</tbody>
</table>

 

当驱动程序的[**取消**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程退出的值**Irp-&gt;CancelIrql**成员不是当前 IRQL。 通常情况下，会出现此错误的驱动程序不会调用[ **IoReleaseCancelSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))所提供的最新的 IRQL 与调用[ **IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))。

有关详细信息*取消*例程，请参阅[取消 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/canceling-irps)。 有关特定于此警告的信息，请参阅[指向考虑时取消 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/points-to-consider-when-canceling-irps)。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的代码示例会引起此警告。

```
IoReleaseCancelSpinLock(PASSIVE_LEVEL);
```

下面的代码示例可避免此警告。

```
IoReleaseCancelSpinLock(Irp->CancelIrql);
```

 

 





