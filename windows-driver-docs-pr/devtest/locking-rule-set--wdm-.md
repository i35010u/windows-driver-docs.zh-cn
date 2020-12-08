---
title: 锁定规则集 (WDM)
description: 使用这些规则验证驱动程序是否正确管理共享资源。
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 23343d6ccd8d2f71e6498da26c256cb392248905
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841289"
---
# <a name="locking-rule-set-wdm"></a>锁定规则集 (WDM)


使用这些规则验证驱动程序是否正确管理共享资源。

## <a name="in-this-section"></a>在本节中


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
<td align="left"><p>CancelSpinLock 规则指定在调用<a href="/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)" data-raw-source="[&lt;strong&gt;IoReleaseCancelSpinLock&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))"><strong>IoReleaseCancelSpinLock</strong></a>之前，驱动程序调用<a href="/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)" data-raw-source="[&lt;strong&gt;IoAcquireCancelSpinLock&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))"><strong>IoAcquireCancelSpinLock</strong></a> ，并且驱动程序会在对<strong>IoAcquireCancelSpinLock</strong>的任何后续调用之前调用<strong>IoReleaseCancelSpinLock</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-cancelspinlockrelease.md" data-raw-source="[&lt;strong&gt;CancelSpinlockRelease&lt;/strong&gt;](wdm-cancelspinlockrelease.md)"><strong>CancelSpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="wdm-cancelspinlockrelease.md" data-raw-source="[&lt;strong&gt;CancelSpinlockRelease&lt;/strong&gt;](wdm-cancelspinlockrelease.md)"><strong>CancelSpinlockRelease</strong></a>规则指定在严格替换中使用对<a href="/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)" data-raw-source="[&lt;strong&gt;IoAcquireCancelSpinLock&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))"><strong>IoAcquireCancelSpinLock</strong></a>和<a href="/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)" data-raw-source="[&lt;strong&gt;IoReleaseCancelSpinLock&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))"><strong>IoReleaseCancelSpinLock</strong></a>的调用。 也就是说，每次调用 <strong>IoAcquireCancelSpinLock</strong> 时，都必须具有对 <strong>IoReleaseCancelSpinLock</strong>的相应调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-criticalregions.md" data-raw-source="[&lt;strong&gt;CriticalRegions&lt;/strong&gt;](wdm-criticalregions.md)"><strong>CriticalRegions</strong></a></p></td>
<td align="left"><p><a href="wdm-criticalregions.md" data-raw-source="[&lt;strong&gt;CriticalRegions&lt;/strong&gt;](wdm-criticalregions.md)"><strong>CriticalRegions</strong></a>规则指定在调用<a href="/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion" data-raw-source="[&lt;strong&gt;KeLeaveCriticalRegion&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)"><strong>KeLeaveCriticalRegion</strong></a>之前驱动程序必须调用<a href="/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion" data-raw-source="[&lt;strong&gt;KeEnterCriticalRegion&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)"><strong>KeEnterCriticalRegion</strong></a> ，并且驱动程序会在对<strong>KeEnterCriticalRegion</strong>的任何后续调用之前调用<strong>KeLeaveCriticalRegion</strong> 。 允许 (嵌套调用。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-exclusiveresourceaccess.md" data-raw-source="[&lt;strong&gt;ExclusiveResourceAccess&lt;/strong&gt;](wdm-exclusiveresourceaccess.md)"><strong>ExclusiveResourceAccess</strong></a></p></td>
<td align="left"><p><a href="wdm-exclusiveresourceaccess.md" data-raw-source="[&lt;strong&gt;ExclusiveResourceAccess&lt;/strong&gt;](wdm-exclusiveresourceaccess.md)"><strong>ExclusiveResourceAccess</strong></a>规则指定在调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite" data-raw-source="[&lt;strong&gt;ExReleaseResourceLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)"><strong>ExReleaseResourceLite</strong></a>或<a href="/previous-versions/ff545585(v=vs.85)" data-raw-source="[&lt;strong&gt;ExReleaseResourceForThreadLite&lt;/strong&gt;](/previous-versions/ff545585(v=vs.85))"><strong>ExReleaseResourceForThreadLite</strong></a>之前，驱动程序调用<a href="/previous-versions/ff544351(v=vs.85)" data-raw-source="[&lt;strong&gt;ExAcquireResourceExclusiveLite&lt;/strong&gt;](/previous-versions/ff544351(v=vs.85))"><strong>ExAcquireResourceExclusiveLite</strong></a> ，并指定驱动程序在对<strong>ExReleaseResourceLite</strong>的任何后续调用之前调用<strong>ExReleaseResourceForThreadLite</strong>或<strong>ExAcquireResourceExclusiveLite</strong> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-guardedregions.md" data-raw-source="[&lt;strong&gt;GuardedRegions&lt;/strong&gt;](wdm-guardedregions.md)"><strong>GuardedRegions</strong></a></p></td>
<td align="left"><p><a href="wdm-guardedregions.md" data-raw-source="[&lt;strong&gt;GuardedRegions&lt;/strong&gt;](wdm-guardedregions.md)"><strong>GuardedRegions</strong></a>规则验证是否在严格替换中使用对<a href="/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keenterguardedregion" data-raw-source="[&lt;strong&gt;KeEnterGuardedRegion&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keenterguardedregion)"><strong>KeEnterGuardedRegion</strong></a>和<a href="/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleaveguardedregion" data-raw-source="[&lt;strong&gt;KeLeaveGuardedRegion&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleaveguardedregion)"><strong>KeLeaveGuardedRegion</strong></a>的调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](wdm-queuedspinlock.md)"><strong>QueuedSpinLock</strong></a></p></td>
<td align="left"><p><a href="wdm-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](wdm-queuedspinlock.md)"><strong>QueuedSpinLock</strong></a>规则指定在调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)"><strong>KeReleaseInStackQueuedSpinLock</strong></a>之前，驱动程序调用<a href="/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLock</strong></a> ，并且驱动程序会在对<strong>KeAcquireInStackQueuedSpinLock</strong>的任何后续调用之前调用<strong>KeReleaseInStackQueuedSpinLock</strong> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-queuedspinlockrelease.md" data-raw-source="[&lt;strong&gt;QueuedSpinLockRelease&lt;/strong&gt;](wdm-queuedspinlockrelease.md)"><strong>QueuedSpinLockRelease</strong></a></p></td>
<td align="left"><p><a href="wdm-queuedspinlockrelease.md" data-raw-source="[&lt;strong&gt;QueuedSpinLockRelease&lt;/strong&gt;](wdm-queuedspinlockrelease.md)"><strong>QueuedSpinLockRelease</strong></a>规则指定在严格替换中使用对<a href="/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLock</strong></a>和<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)"><strong>KeReleaseInStackQueuedSpinLock</strong></a>的调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](wdm-spinlock.md)"><strong>SpinLock</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](wdm-spinlock.md)"><strong>旋转锁</strong></a>规则指定在调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)"><strong>KeAcquireSpinLock</strong></a>之后，驱动程序调用<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinLock</strong></a> ，然后再调用<strong>KeAcquireSpinLock</strong>或<a href="/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"><strong>KeAcquireSpinLockRaiseToDpc</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinLockDpc&lt;/strong&gt;](wdm-spinlockdpc.md)"><strong>SpinLockDpc</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinLockDpc&lt;/strong&gt;](wdm-spinlockdpc.md)"><strong>SpinLockDpc</strong></a>规则指定对<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)"><strong>KeAcquireSpinLock</strong></a>或<a href="/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"><strong>KeAcquireSpinLockRaiseToDpc</strong></a>和<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinLock</strong></a>的调用必须在严格替换中进行。 也就是说，在调用 <strong>KeAcquireSpinLock</strong> 或 <strong>KeAcquireSpinLockRaiseToDpc</strong>之后，驱动程序必须先调用 <strong>KeReleaseSpinLock</strong> ，然后再调用 <strong>KeAcquireSpinLock</strong> 或 <strong>KeAcquireSpinLockRaiseToDpc</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](wdm-spinlockrelease.md)"><strong>SpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](wdm-spinlockrelease.md)"><strong>SpinlockRelease</strong></a>规则指定对<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinLock</strong></a>的调用是在严格替换<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)"><strong>KeAcquireSpinLock</strong></a>和<a href="/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"><strong>KeAcquireSpinLockRaiseToDpc</strong></a>时进行的。 也就是说，驱动程序必须在调用<strong>KeAcquireSpinLock</strong>或<strong>KeAcquireSpinLockRaiseToDpc</strong>后，在后续调用<strong>KeAcquireSpinLock</strong>或<strong>KeAcquireSpinLockRaiseToDpc</strong>之前调用<strong>KeReleaseSpinLock</strong> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-spinlocksafe.md" data-raw-source="[&lt;strong&gt;SpinLockSafe&lt;/strong&gt;](wdm-spinlocksafe.md)"><strong>SpinLockSafe</strong></a></p></td>
<td align="left"><p><a href="wdm-spinlocksafe.md" data-raw-source="[&lt;strong&gt;SpinLockSafe&lt;/strong&gt;](wdm-spinlocksafe.md)"><strong>SpinLockSafe</strong></a>规则指定在保存旋转锁时不调用<a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket" data-raw-source="[&lt;strong&gt;IoStartNextPacket&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)"><strong>IoStartNextPacket</strong></a>和<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-withincriticalregion.md" data-raw-source="[&lt;strong&gt;WithinCriticalRegion&lt;/strong&gt;](wdm-withincriticalregion.md)"><strong>WithinCriticalRegion</strong></a></p></td>
<td align="left"><p><a href="wdm-withincriticalregion.md" data-raw-source="[&lt;strong&gt;WithinCriticalRegion&lt;/strong&gt;](wdm-withincriticalregion.md)"><strong>WithinCriticalRegion</strong></a>规则指定仅在调用<a href="/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion" data-raw-source="[&lt;strong&gt;KeEnterCriticalRegion&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)"><strong>KeEnterCriticalRegion</strong></a>之后和调用<a href="/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion" data-raw-source="[&lt;strong&gt;KeLeaveCriticalRegion&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)"><strong>KeLeaveCriticalRegion</strong></a>之前，对特定同步函数的调用才会出现。</p>
<p>受影响的同步函数如下所示：</p>
<ul>
<li><p><a href="/previous-versions/ff544363(v=vs.85)" data-raw-source="[&lt;strong&gt;ExAcquireResourceSharedLite&lt;/strong&gt;](/previous-versions/ff544363(v=vs.85))"><strong>ExAcquireResourceSharedLite</strong></a></p></li>
<li><p><a href="/previous-versions/ff544351(v=vs.85)" data-raw-source="[&lt;strong&gt;ExAcquireResourceExclusiveLite&lt;/strong&gt;](/previous-versions/ff544351(v=vs.85))"><strong>ExAcquireResourceExclusiveLite</strong></a></p></li>
<li><p><a href="/previous-versions/ff544367(v=vs.85)" data-raw-source="[&lt;strong&gt;ExAcquireSharedStarveExclusive&lt;/strong&gt;](/previous-versions/ff544367(v=vs.85))"><strong>ExAcquireSharedStarveExclusive</strong></a></p></li>
<li><p><a href="/previous-versions/ff544370(v=vs.85)" data-raw-source="[&lt;strong&gt;ExAcquireSharedWaitForExclusive&lt;/strong&gt;](/previous-versions/ff544370(v=vs.85))"><strong>ExAcquireSharedWaitForExclusive</strong></a></p></li>
<li><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite" data-raw-source="[&lt;strong&gt;ExReleaseResourceLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)"><strong>ExReleaseResourceLite</strong></a></p></li>
<li><p><a href="/previous-versions/ff545585(v=vs.85)" data-raw-source="[&lt;strong&gt;ExReleaseResourceForThreadLite&lt;/strong&gt;](/previous-versions/ff545585(v=vs.85))"><strong>ExReleaseResourceForThreadLite</strong></a></p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**选择锁定规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **锁定**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check** 选项指定 **sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Locking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

