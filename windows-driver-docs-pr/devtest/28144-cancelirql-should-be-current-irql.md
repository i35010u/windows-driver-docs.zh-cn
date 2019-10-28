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
ms.openlocfilehash: 434868c580adb4b4f9de52d9698b24f9338bf1a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839593"
---
# <a name="c28144"></a>C28144


警告 C28144：在 "取消" 例程内，在退出时，Irp&gt;Irp->cancelirql 中的 IRQL 应为当前的 IRQL。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>附加信息</strong></p></td>
<td align="left"><p>此值不需要由任何特定函数还原，但必须在退出前还原。 PREfast 无法确定它是否已还原为所需的值。</p></td>
</tr>
</tbody>
</table>

 

当驱动程序的[**Cancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程退出时， **Irp&gt;irp->cancelirql**成员的值不是当前的 IRQL。 通常情况下，当驱动程序未使用由最新的[**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))调用提供的 IRQL 调用[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))时，会发生此错误。

有关*取消*例程的详细信息，请参阅[取消 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/canceling-irps)。 有关特定于此警告的信息，请参阅[取消 Irp 时要考虑的要点](https://docs.microsoft.com/windows-hardware/drivers/kernel/points-to-consider-when-canceling-irps)。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>实例

下面的代码示例 elicits 此警告。

```
IoReleaseCancelSpinLock(PASSIVE_LEVEL);
```

下面的代码示例可避免此警告。

```
IoReleaseCancelSpinLock(Irp->CancelIrql);
```

 

 





