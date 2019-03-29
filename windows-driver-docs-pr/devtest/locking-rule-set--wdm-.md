---
title: 锁定规则集 (WDM)
description: 使用这些规则来验证您的驱动程序正确管理共享的资源。
ms.assetid: B23863BD-66F0-4E6F-B150-97FD2066F69C
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: b5d7b3b00888327ec27402edaabf849aa6c3544a
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349524"
---
# <a name="locking-rule-set-wdm"></a>锁定规则集 (WDM)


使用这些规则来验证您的驱动程序正确管理共享的资源。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="wdm-cancelspinlock.md" data-raw-source="[&lt;strong&gt;CancelSpinLock&lt;/strong&gt;](wdm-cancelspinlock.md)"><strong>CancelSpinLock</strong></a></p></td>
<td align="left"><p>CancelSpinLock 规则指定驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548196" data-raw-source="[&lt;strong&gt;IoAcquireCancelSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548196)"> <strong>IoAcquireCancelSpinLock</strong> </a>之前调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549550" data-raw-source="[&lt;strong&gt;IoReleaseCancelSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549550)"> <strong>IoReleaseCancelSpinLock</strong> </a>和驱动程序调用<strong>IoReleaseCancelSpinLock</strong>之前对任何后续调用<strong>IoAcquireCancelSpinLock</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-cancelspinlockrelease.md" data-raw-source="[&lt;strong&gt;CancelSpinlockRelease&lt;/strong&gt;](wdm-cancelspinlockrelease.md)"><strong>CancelSpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="wdm-cancelspinlockrelease.md" data-raw-source="[&lt;strong&gt;CancelSpinlockRelease&lt;/strong&gt;](wdm-cancelspinlockrelease.md)"> <strong>CancelSpinlockRelease</strong> </a>规则指定的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548196" data-raw-source="[&lt;strong&gt;IoAcquireCancelSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548196)"> <strong>IoAcquireCancelSpinLock</strong> </a>和<a href="https://msdn.microsoft.com/library/windows/hardware/ff549550" data-raw-source="[&lt;strong&gt;IoReleaseCancelSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549550)"> <strong>IoReleaseCancelSpinLock</strong> </a>严格的分支结构中使用。 也就是说，每次调用<strong>IoAcquireCancelSpinLock</strong>必须具有相应地调用<strong>IoReleaseCancelSpinLock</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-criticalregions.md" data-raw-source="[&lt;strong&gt;CriticalRegions&lt;/strong&gt;](wdm-criticalregions.md)"><strong>CriticalRegions</strong></a></p></td>
<td align="left"><p><a href="wdm-criticalregions.md" data-raw-source="[&lt;strong&gt;CriticalRegions&lt;/strong&gt;](wdm-criticalregions.md)"> <strong>CriticalRegions</strong> </a>规则指定驱动程序必须调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff552021" data-raw-source="[&lt;strong&gt;KeEnterCriticalRegion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552021)"> <strong>KeEnterCriticalRegion</strong> </a>之前调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff552964" data-raw-source="[&lt;strong&gt;KeLeaveCriticalRegion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552964)"><strong>KeLeaveCriticalRegion</strong> </a>和驱动程序调用<strong>KeLeaveCriticalRegion</strong>之前对任何后续调用<strong>KeEnterCriticalRegion</strong>. （允许嵌套的调用。）</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-exclusiveresourceaccess.md" data-raw-source="[&lt;strong&gt;ExclusiveResourceAccess&lt;/strong&gt;](wdm-exclusiveresourceaccess.md)"><strong>ExclusiveResourceAccess</strong></a></p></td>
<td align="left"><p><a href="wdm-exclusiveresourceaccess.md" data-raw-source="[&lt;strong&gt;ExclusiveResourceAccess&lt;/strong&gt;](wdm-exclusiveresourceaccess.md)"> <strong>ExclusiveResourceAccess</strong> </a>规则指定驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544351" data-raw-source="[&lt;strong&gt;ExAcquireResourceExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544351)"> <strong>ExAcquireResourceExclusiveLite</strong> </a>之前调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545597" data-raw-source="[&lt;strong&gt;ExReleaseResourceLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545597)"> <strong>ExReleaseResourceLite</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff545585" data-raw-source="[&lt;strong&gt;ExReleaseResourceForThreadLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545585)"> <strong>ExReleaseResourceForThreadLite</strong> </a> ，并指定驱动程序调用<strong>ExReleaseResourceLite</strong>或<strong>ExReleaseResourceForThreadLite</strong>之前对任何后续调用<strong>ExAcquireResourceExclusiveLite</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-guardedregions.md" data-raw-source="[&lt;strong&gt;GuardedRegions&lt;/strong&gt;](wdm-guardedregions.md)"><strong>GuardedRegions</strong></a></p></td>
<td align="left"><p><a href="wdm-guardedregions.md" data-raw-source="[&lt;strong&gt;GuardedRegions&lt;/strong&gt;](wdm-guardedregions.md)"> <strong>GuardedRegions</strong> </a>规则验证的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff552028" data-raw-source="[&lt;strong&gt;KeEnterGuardedRegion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552028)"> <strong>KeEnterGuardedRegion</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff552967" data-raw-source="[&lt;strong&gt;KeLeaveGuardedRegion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552967)"> <strong>KeLeaveGuardedRegion</strong> </a>严格的分支结构中使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](wdm-queuedspinlock.md)"><strong>QueuedSpinLock</strong></a></p></td>
<td align="left"><p><a href="wdm-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](wdm-queuedspinlock.md)"> <strong>QueuedSpinLock</strong> </a>规则指定驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff551899" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551899)"> <strong>KeAcquireInStackQueuedSpinLock</strong> </a>调用前<a href="https://msdn.microsoft.com/library/windows/hardware/ff553130" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553130)"> <strong>KeReleaseInStackQueuedSpinLock</strong> </a>和驱动程序调用<strong>KeReleaseInStackQueuedSpinLock</strong>之前对任何后续调用<strong>KeAcquireInStackQueuedSpinLock</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-queuedspinlockrelease.md" data-raw-source="[&lt;strong&gt;QueuedSpinLockRelease&lt;/strong&gt;](wdm-queuedspinlockrelease.md)"><strong>QueuedSpinLockRelease</strong></a></p></td>
<td align="left"><p><a href="wdm-queuedspinlockrelease.md" data-raw-source="[&lt;strong&gt;QueuedSpinLockRelease&lt;/strong&gt;](wdm-queuedspinlockrelease.md)"> <strong>QueuedSpinLockRelease</strong> </a>规则指定的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff551899" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551899)"> <strong>KeAcquireInStackQueuedSpinLock</strong> </a>和<a href="https://msdn.microsoft.com/library/windows/hardware/ff553130" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553130)"> <strong>KeReleaseInStackQueuedSpinLock</strong> </a>严格的分支结构中使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](wdm-spinlock.md)"><strong>SpinLock</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](wdm-spinlock.md)"><strong>旋转锁</strong></a>规则指定的在调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff551917" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551917)"> <strong>KeAcquireSpinLock</strong></a>，驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff553145" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553145)"> <strong>KeReleaseSpinLock</strong> </a>之前对后续调用<strong>KeAcquireSpinLock</strong>或设置为<a href="https://msdn.microsoft.com/library/windows/hardware/ff551928" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551928)"> <strong>KeAcquireSpinLockRaiseToDpc</strong> </a>.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinLockDpc&lt;/strong&gt;](wdm-spinlockdpc.md)"><strong>SpinLockDpc</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinLockDpc&lt;/strong&gt;](wdm-spinlockdpc.md)"> <strong>SpinLockDpc</strong> </a>规则指定的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff551917" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551917)"> <strong>KeAcquireSpinLock</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff551928" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551928)"> <strong>KeAcquireSpinLockRaiseToDpc</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff553145" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553145)"> <strong>KeReleaseSpinLock</strong> </a>必须在严格的分支结构中进行。 也就是说，之后调用<strong>KeAcquireSpinLock</strong>或<strong>KeAcquireSpinLockRaiseToDpc</strong>，该驱动程序必须调用<strong>KeReleaseSpinLock</strong>之前对的后续调用<strong>KeAcquireSpinLock</strong>或设置为<strong>KeAcquireSpinLockRaiseToDpc</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](wdm-spinlockrelease.md)"><strong>SpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](wdm-spinlockrelease.md)"> <strong>SpinlockRelease</strong> </a>规则指定的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff553145" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553145)"> <strong>KeReleaseSpinLock</strong> </a> 与逻辑或strict中所做<a href="https://msdn.microsoft.com/library/windows/hardware/ff551917" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551917)"> <strong>KeAcquireSpinLock</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff551928" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551928)"> <strong>KeAcquireSpinLockRaiseToDpc</strong></a>。 也就是说，该驱动程序必须调用<strong>KeReleaseSpinLock</strong>后调用<strong>KeAcquireSpinLock</strong>或<strong>KeAcquireSpinLockRaiseToDpc</strong>之前对的后续调用<strong>KeAcquireSpinLock</strong>或设置为<strong>KeAcquireSpinLockRaiseToDpc</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-spinlocksafe.md" data-raw-source="[&lt;strong&gt;SpinLockSafe&lt;/strong&gt;](wdm-spinlocksafe.md)"><strong>SpinLockSafe</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlocksafe.md" data-raw-source="[&lt;strong&gt;SpinLockSafe&lt;/strong&gt;](wdm-spinlocksafe.md)"> <strong>SpinLockSafe</strong> </a>规则指定<a href="https://msdn.microsoft.com/library/windows/hardware/ff550358" data-raw-source="[&lt;strong&gt;IoStartNextPacket&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550358)"> <strong>IoStartNextPacket</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff548343" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548343)"> <strong>IoCompleteRequest</strong> </a>不会占用自旋锁时调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-withincriticalregion.md" data-raw-source="[&lt;strong&gt;WithinCriticalRegion&lt;/strong&gt;](wdm-withincriticalregion.md)"><strong>WithinCriticalRegion</strong></a></p></td>
<td align="left"><p><a href="wdm-withincriticalregion.md" data-raw-source="[&lt;strong&gt;WithinCriticalRegion&lt;/strong&gt;](wdm-withincriticalregion.md)"> <strong>WithinCriticalRegion</strong> </a>规则指定对特定同步函数的驱动程序的调用出现在调用后才<a href="https://msdn.microsoft.com/library/windows/hardware/ff552021" data-raw-source="[&lt;strong&gt;KeEnterCriticalRegion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552021)"> <strong>KeEnterCriticalRegion</strong> </a> ，然后再调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff552964" data-raw-source="[&lt;strong&gt;KeLeaveCriticalRegion&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552964)"> <strong>KeLeaveCriticalRegion</strong></a>。</p>
<p>受影响的同步函数如下所示：</p>
<ul>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544363" data-raw-source="[&lt;strong&gt;ExAcquireResourceSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544363)"><strong>ExAcquireResourceSharedLite</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544351" data-raw-source="[&lt;strong&gt;ExAcquireResourceExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544351)"><strong>ExAcquireResourceExclusiveLite</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544367" data-raw-source="[&lt;strong&gt;ExAcquireSharedStarveExclusive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544367)"><strong>ExAcquireSharedStarveExclusive</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544370" data-raw-source="[&lt;strong&gt;ExAcquireSharedWaitForExclusive&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544370)"><strong>ExAcquireSharedWaitForExclusive</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545597" data-raw-source="[&lt;strong&gt;ExReleaseResourceLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545597)"><strong>ExReleaseResourceLite</strong></a></p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545585" data-raw-source="[&lt;strong&gt;ExReleaseResourceForThreadLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545585)"><strong>ExReleaseResourceForThreadLite</strong></a></p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**若要选择的锁定规则设置**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...**.

2.  单击**规则**选项卡。下**规则集**，选择**锁定**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**Locking.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Locking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/hh454281)并[Static Driver Verifier 命令 (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)。

 

 





