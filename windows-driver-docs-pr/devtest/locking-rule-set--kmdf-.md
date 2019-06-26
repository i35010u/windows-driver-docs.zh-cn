---
title: 锁定规则集 (KMDF)
description: 使用这些规则来验证您的驱动程序正确管理共享的资源。
ms.assetid: B6DD41A5-E7E5-4070-8752-68E26804A5D5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2879b913defa88cc1c0907c2c718eaa3dfd7edb2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354789"
---
# <a name="locking-rule-set-kmdf"></a>锁定规则集 (KMDF)


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
<td align="left"><p><a href="kmdf-parentobjectchecklock.md" data-raw-source="[&lt;strong&gt;ParentObjectCheckLock&lt;/strong&gt;](kmdf-parentobjectchecklock.md)"><strong>ParentObjectCheckLock</strong></a></p></td>
<td align="left"><p><a href="kmdf-parentobjectchecklock.md" data-raw-source="[&lt;strong&gt;ParentObjectCheckLock&lt;/strong&gt;](kmdf-parentobjectchecklock.md)"> <strong>ParentObjectCheckLock</strong> </a>规则指定驱动程序应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfwaitlockcreate" data-raw-source="[&lt;strong&gt;WdfWaitLockCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfwaitlockcreate)"> <strong>WdfWaitLockCreate</strong> </a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfspinlockcreate" data-raw-source="[&lt;strong&gt;WdfSpinLockCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfspinlockcreate)"> <strong>WdfSpinLockCreate</strong> </a>设置父对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqsendwhilespinlock.md" data-raw-source="[&lt;strong&gt;ReqSendWhileSpinlock&lt;/strong&gt;](kmdf-reqsendwhilespinlock.md)"><strong>ReqSendWhileSpinlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqsendwhilespinlock.md" data-raw-source="[&lt;strong&gt;ReqSendWhileSpinlock&lt;/strong&gt;](kmdf-reqsendwhilespinlock.md)"> <strong>ReqSendWhileSpinlock</strong> </a>规则指定驱动程序包含自旋锁时发送了任何请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-spinlock.md" data-raw-source="[&lt;strong&gt;Spinlock&lt;/strong&gt;](kmdf-spinlock.md)"><strong>Spinlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-spinlock.md" data-raw-source="[&lt;strong&gt;Spinlock&lt;/strong&gt;](kmdf-spinlock.md)"><strong>旋转锁</strong></a>规则指定的调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)"> <strong>KeAcquireSpinLock</strong> </a>或<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"> <strong>KeAcquireSpinLockRaiseToDpc</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)"> <strong>KeReleaseSpinlock</strong> </a>严格的分支结构中使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinlockDpc&lt;/strong&gt;](kmdf-spinlockdpc.md)"><strong>SpinlockDpc</strong></a></p></td>
<td align="left"><p><a href="kmdf-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinlockDpc&lt;/strong&gt;](kmdf-spinlockdpc.md)"> <strong>SpinlockDpc</strong> </a>规则指定的调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)"> <strong>KeAcquireSpinLock</strong> </a>或<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"> <strong>KeAcquireSpinLockRaiseToDpc</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)"> <strong>KeReleaseSpinlock</strong> </a>严格的分支结构中使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](kmdf-spinlockrelease.md)"><strong>SpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](kmdf-spinlockrelease.md)"> <strong>SpinlockRelease</strong> </a>规则指定的调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)"> <strong>KeAcquireSpinLock</strong></a>， <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"> <strong>KeAcquireSpinLockRaiseToDpc</strong></a>，并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)"> <strong>KeReleaseSpinLock</strong> </a> KMDF 回调中以平衡方式使用。 在任何 KMDF 回调例程结束时，该驱动程序不应阻止自旋锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfinterruptlock.md" data-raw-source="[&lt;strong&gt;WdfInterruptLock&lt;/strong&gt;](kmdf-wdfinterruptlock.md)"><strong>WdfInterruptLock</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfinterruptlock.md" data-raw-source="[&lt;strong&gt;WdfInterruptLock&lt;/strong&gt;](kmdf-wdfinterruptlock.md)"> <strong>WdfInterruptLock</strong> </a>规则指定的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff547340" data-raw-source="[&lt;strong&gt;WdfInterruptAcquireLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547340)"> <strong>WdfInterruptAcquireLock</strong> </a>中使用逻辑或严格使用方法调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff547376" data-raw-source="[&lt;strong&gt;WdfInterruptReleaseLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547376)"> <strong>WdfInterruptReleaseLock</strong></a>。 此外，在任何 KMDF 回调例程结束时，该驱动程序不应阻止 framework 数值调节钮锁对象，通过以前调用获得<strong>WdfInterruptAcquireLock</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfinterruptlockrelease.md" data-raw-source="[&lt;strong&gt;WdfInterruptLockRelease&lt;/strong&gt;](kmdf-wdfinterruptlockrelease.md)"><strong>WdfInterruptLockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfinterruptlockrelease.md" data-raw-source="[&lt;strong&gt;WdfInterruptLockRelease&lt;/strong&gt;](kmdf-wdfinterruptlockrelease.md)"> <strong>WdfInterruptLockRelease</strong> </a>规则指定的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff547340" data-raw-source="[&lt;strong&gt;WdfInterruptAcquireLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547340)"> <strong>WdfInterruptAcquireLock</strong> </a>和<a href="https://msdn.microsoft.com/library/windows/hardware/ff547376" data-raw-source="[&lt;strong&gt;WdfInterruptReleaseLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547376)"> <strong>WdfInterruptReleaseLock</strong> </a> KMDF 回调例程中以平衡方式使用。 在任何 KMDF 回调例程结束时，该驱动程序不应阻止通过以前调用获得的 framework 自旋锁对象<strong>WdfInterruptAcquireLock</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfspinlock.md" data-raw-source="[&lt;strong&gt;WdfSpinlock&lt;/strong&gt;](kmdf-wdfspinlock.md)"><strong>WdfSpinlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfspinlock.md" data-raw-source="[&lt;strong&gt;WdfSpinlock&lt;/strong&gt;](kmdf-wdfspinlock.md)"> <strong>WdfSpinlock</strong> </a>规则指定的调用<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)" data-raw-source="[&lt;strong&gt;WdfSpinLockAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))"> <strong>WdfSpinLockAcquire</strong> </a>中具有逻辑或严格使用方法<a href="kmdf-wdfspinlockrelease.md" data-raw-source="[&lt;strong&gt;WdfSpinlockRelease&lt;/strong&gt;](kmdf-wdfspinlockrelease.md)"><strong>WdfSpinlockRelease</strong></a>。 在任何 KMDF 回调例程结束时，该驱动程序不应阻止 framework 旋转锁对象，它通过以前调用获得<strong>WdfSpinLockAcquire</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfspinlockrelease.md" data-raw-source="[&lt;strong&gt;WdfSpinlockRelease&lt;/strong&gt;](kmdf-wdfspinlockrelease.md)"><strong>WdfSpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfspinlockrelease.md" data-raw-source="[&lt;strong&gt;WdfSpinlockRelease&lt;/strong&gt;](kmdf-wdfspinlockrelease.md)"> <strong>WdfSpinlockRelease</strong> </a>规则指定的调用<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)" data-raw-source="[&lt;strong&gt;WdfSpinLockAcquire&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))"> <strong>WdfSpinLockAcquire</strong> </a>和<strong>WdfSpinlockRelease</strong> KMDF 事件回调函数中以平衡方式使用。 KMDF 事件回调函数返回时，该驱动程序不应阻止通过以前调用获得的 framework 自旋锁对象<strong>WdfSpinLockAcquire</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfwaitlock.md" data-raw-source="[&lt;strong&gt;WdfWaitlock&lt;/strong&gt;](kmdf-wdfwaitlock.md)"><strong>WdfWaitlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfwaitlock.md" data-raw-source="[&lt;strong&gt;WdfWaitlock&lt;/strong&gt;](kmdf-wdfwaitlock.md)"> <strong>WdfWaitlock</strong> </a>规则指定的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff551168" data-raw-source="[&lt;strong&gt;WdfWaitLockAcquire&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551168)"> <strong>WdfWaitLockAcquire</strong> </a>中使用逻辑或严格使用<a href="kmdf-wdfwaitlockrelease.md" data-raw-source="[&lt;strong&gt;WdfWaitlockRelease&lt;/strong&gt;](kmdf-wdfwaitlockrelease.md)"><strong>WdfWaitlockRelease</strong></a>。 KMDF 事件回调函数返回时，该驱动程序不应阻止通过以前调用获得的 framework 自旋锁对象<strong>WdfWaitLockAcquire</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfwaitlockrelease.md" data-raw-source="[&lt;strong&gt;WdfWaitlockRelease&lt;/strong&gt;](kmdf-wdfwaitlockrelease.md)"><strong>WdfWaitlockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfwaitlockrelease.md" data-raw-source="[&lt;strong&gt;WdfWaitlockRelease&lt;/strong&gt;](kmdf-wdfwaitlockrelease.md)"> <strong>WdfWaitlockRelease</strong> </a>规则指定的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff551168" data-raw-source="[&lt;strong&gt;WdfWaitLockAcquire&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551168)"> <strong>WdfWaitLockAcquire</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfwaitlockrelease" data-raw-source="[&lt;strong&gt;WdfWaitLockRelease&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfwaitlockrelease)"> <strong>WdfWaitLockRelease</strong> </a> KMDF 事件回调函数中以平衡方式使用。 KMDF 事件回调函数返回时，该驱动程序不应阻止通过以前调用获得的 framework 自旋锁对象<strong>WdfWaitLockAcquire</strong>。</p></td>
</tr>
</tbody>
</table>

 

**若要选择的锁定规则设置**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**锁定**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**Locking.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Locking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





