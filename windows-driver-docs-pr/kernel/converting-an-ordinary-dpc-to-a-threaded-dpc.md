---
title: 将普通 DPC 转换为线程 DPC
description: 将普通 DPC 转换为线程 DPC
ms.assetid: 89a7a408-e01b-4543-9775-5ef542d05b75
keywords:
- 线程 Dpc WDK 内核
- 转换 Dpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7075c4035b6e2a2965e538ebe5d198a981e9db5a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189821"
---
# <a name="converting-an-ordinary-dpc-to-a-threaded-dpc"></a>将普通 DPC 转换为线程 DPC





将普通 DPC 转换为螺纹 DPC 非常简单。 只需替换对 [**KeInitializeDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc) (的调用，该调用会将 dpc) 替换为一到 [**KeInitializeThreadedDpc**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializethreadeddpc)，并参考下表来替换 dpc 例程内获取和释放自旋锁的调用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>普通 DPC 调用</th>
<th>对应的线程 DPC 调用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockAtDpcLevel&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)"><strong>KeAcquireSpinLockAtDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551923(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockForDpc&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff551923(v=vs.85))"><strong>KeAcquireSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel" data-raw-source="[&lt;strong&gt;KeReleaseSpinLockFromDpcLevel&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)"><strong>KeReleaseSpinLockFromDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfordpc" data-raw-source="[&lt;strong&gt;KeReleaseSpinLockForDpc&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfordpc)"><strong>KeReleaseSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockAtDpcLevel&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551912(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockForDpc&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff551912(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockFromDpcLevel&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)"><strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockForDpc&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc)"><strong>KeReleaseInStackQueuedSpinLockForDpc</strong></a></p></td>
</tr>
</tbody>
</table>

 

不需要更改对其他自旋锁例程（如 [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 或 [**KeAcquireInStackQueuedSpinLock**](/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))）的调用。

 

