---
title: 将普通 DPC 转换为线程 DPC
description: 将普通 DPC 转换为线程 DPC
ms.assetid: 89a7a408-e01b-4543-9775-5ef542d05b75
keywords:
- 线程的 Dpc WDK 内核
- 转换 dpc 进行标记
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1aa526289ef27c6f6e91bb0d6d66fc15aa49a198
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348250"
---
# <a name="converting-an-ordinary-dpc-to-a-threaded-dpc"></a>将普通 DPC 转换为线程 DPC





将普通 DPC 转换为线程 DPC 非常简单。 只需替换为对[ **KeInitializeDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552130) （初始化 DPC） 使用一到[ **KeInitializeThreadedDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552166)，并参考下表来替换 DPC 例程中的调用的获取和释放自旋锁。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>普通 DPC 调用</th>
<th>相应线程的 DPC 调用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551921" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockAtDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551921)"><strong>KeAcquireSpinLockAtDpcLevel</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551923" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockForDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551923)"><strong>KeAcquireSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553150" data-raw-source="[&lt;strong&gt;KeReleaseSpinLockFromDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553150)"><strong>KeReleaseSpinLockFromDpcLevel</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553148" data-raw-source="[&lt;strong&gt;KeReleaseSpinLockForDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553148)"><strong>KeReleaseSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551908" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockAtDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551908)"><strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551912" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockForDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551912)"><strong>KeAcquireInStackQueuedSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553137" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockFromDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553137)"><strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553133" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockForDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553133)"><strong>KeReleaseInStackQueuedSpinLockForDpc</strong></a></p></td>
</tr>
</tbody>
</table>

 

不需要更改对其他数值调节钮锁定例程，例如[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)或[ **KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899).

 

 




