---
title: 将普通 DPC 转换为线程 DPC
description: 将普通 DPC 转换为线程 DPC
ms.assetid: 89a7a408-e01b-4543-9775-5ef542d05b75
keywords:
- 线程 Dpc WDK 内核
- 转换 Dpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c924affbb4d81c416c79731468e84250c277ac7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828475"
---
# <a name="converting-an-ordinary-dpc-to-a-threaded-dpc"></a>将普通 DPC 转换为线程 DPC





将普通 DPC 转换为螺纹 DPC 非常简单。 只需将对[**KeInitializeDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc) （这会初始化 DPC）的调用替换为一到[**KeInitializeThreadedDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializethreadeddpc)，然后参考下表来替换 DPC 例程内获取和释放自旋锁的调用。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockAtDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)"><strong>KeAcquireSpinLockAtDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551923(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockForDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551923(v=vs.85))"><strong>KeAcquireSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel" data-raw-source="[&lt;strong&gt;KeReleaseSpinLockFromDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)"><strong>KeReleaseSpinLockFromDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfordpc" data-raw-source="[&lt;strong&gt;KeReleaseSpinLockForDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfordpc)"><strong>KeReleaseSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockAtDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551912(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockForDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551912(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockFromDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)"><strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockForDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc)"><strong>KeReleaseInStackQueuedSpinLockForDpc</strong></a></p></td>
</tr>
</tbody>
</table>

 

不需要更改对其他自旋锁例程（如[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)或[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))）的调用。

 

 




