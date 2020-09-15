---
title: 锁定规则集 (KMDF)
description: 使用这些规则验证驱动程序是否正确管理共享资源。
ms.assetid: B6DD41A5-E7E5-4070-8752-68E26804A5D5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1e7be62baeb424f7a8ab10a0be029fcf02d56277
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103408"
---
# <a name="locking-rule-set-kmdf"></a>锁定规则集 (KMDF)


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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="kmdf-parentobjectchecklock.md" data-raw-source="[&lt;strong&gt;ParentObjectCheckLock&lt;/strong&gt;](kmdf-parentobjectchecklock.md)"><strong>ParentObjectCheckLock</strong></a></p></td>
<td align="left"><p><a href="kmdf-parentobjectchecklock.md" data-raw-source="[&lt;strong&gt;ParentObjectCheckLock&lt;/strong&gt;](kmdf-parentobjectchecklock.md)"><strong>ParentObjectCheckLock</strong></a>规则指定驱动程序应调用<a href="/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockcreate" data-raw-source="[&lt;strong&gt;WdfWaitLockCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockcreate)"><strong>WdfWaitLockCreate</strong></a> ，并将<a href="/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfspinlockcreate" data-raw-source="[&lt;strong&gt;WdfSpinLockCreate&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfspinlockcreate)"><strong>WdfSpinLockCreate</strong></a>设置为父对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-reqsendwhilespinlock.md" data-raw-source="[&lt;strong&gt;ReqSendWhileSpinlock&lt;/strong&gt;](kmdf-reqsendwhilespinlock.md)"><strong>ReqSendWhileSpinlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-reqsendwhilespinlock.md" data-raw-source="[&lt;strong&gt;ReqSendWhileSpinlock&lt;/strong&gt;](kmdf-reqsendwhilespinlock.md)"><strong>ReqSendWhileSpinlock</strong></a>规则指定在驱动程序持有旋转锁时不发送请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-spinlock.md" data-raw-source="[&lt;strong&gt;Spinlock&lt;/strong&gt;](kmdf-spinlock.md)"><strong>旋转锁</strong></a></p></td>
<td align="left"><p><a href="kmdf-spinlock.md" data-raw-source="[&lt;strong&gt;Spinlock&lt;/strong&gt;](kmdf-spinlock.md)"><strong>旋转锁</strong></a>规则指定在严格替换中使用对<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)"><strong>KeAcquireSpinLock</strong></a> 、 <a href="/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"><strong>KeAcquireSpinLockRaiseToDpc</strong></a>和<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinlock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinlock</strong></a>的调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinlockDpc&lt;/strong&gt;](kmdf-spinlockdpc.md)"><strong>SpinlockDpc</strong></a></p></td>
<td align="left"><p><a href="kmdf-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinlockDpc&lt;/strong&gt;](kmdf-spinlockdpc.md)"><strong>SpinlockDpc</strong></a>规则指定在严格替换中使用对<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)"><strong>KeAcquireSpinLock</strong></a> 、 <a href="/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"><strong>KeAcquireSpinLockRaiseToDpc</strong></a>和<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinlock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinlock</strong></a>的调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](kmdf-spinlockrelease.md)"><strong>SpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinlockRelease&lt;/strong&gt;](kmdf-spinlockrelease.md)"><strong>SpinlockRelease</strong></a>规则指定对<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock" data-raw-source="[&lt;strong&gt;KeAcquireSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)"><strong>KeAcquireSpinLock</strong></a>、 <a href="/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockRaiseToDpc&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))"><strong>KeAcquireSpinLockRaiseToDpc</strong></a>和<a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)"><strong>KeReleaseSpinLock</strong></a>的调用在 KMDF 回调内以均衡方式使用。 在任何 KMDF 回调例程结束时，驱动程序不应持有自旋锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfinterruptlock.md" data-raw-source="[&lt;strong&gt;WdfInterruptLock&lt;/strong&gt;](kmdf-wdfinterruptlock.md)"><strong>WdfInterruptLock</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfinterruptlock.md" data-raw-source="[&lt;strong&gt;WdfInterruptLock&lt;/strong&gt;](kmdf-wdfinterruptlock.md)"><strong>WdfInterruptLock</strong></a>规则指定对<a href="/previous-versions/ff547340(v=vs.85)" data-raw-source="[&lt;strong&gt;WdfInterruptAcquireLock&lt;/strong&gt;](/previous-versions/ff547340(v=vs.85))"><strong>WdfInterruptAcquireLock</strong></a>方法的调用在严格替换中用于对<a href="/previous-versions/ff547376(v=vs.85)" data-raw-source="[&lt;strong&gt;WdfInterruptReleaseLock&lt;/strong&gt;](/previous-versions/ff547376(v=vs.85))"><strong>WdfInterruptReleaseLock</strong></a>的调用。 此外，在任何 KMDF 回调例程结束时，驱动程序不应持有框架旋转锁对象，这是由先前对 <strong>WdfInterruptAcquireLock</strong>的调用获得的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfinterruptlockrelease.md" data-raw-source="[&lt;strong&gt;WdfInterruptLockRelease&lt;/strong&gt;](kmdf-wdfinterruptlockrelease.md)"><strong>WdfInterruptLockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfinterruptlockrelease.md" data-raw-source="[&lt;strong&gt;WdfInterruptLockRelease&lt;/strong&gt;](kmdf-wdfinterruptlockrelease.md)"><strong>WdfInterruptLockRelease</strong></a>规则指定对<a href="/previous-versions/ff547340(v=vs.85)" data-raw-source="[&lt;strong&gt;WdfInterruptAcquireLock&lt;/strong&gt;](/previous-versions/ff547340(v=vs.85))"><strong>WdfInterruptAcquireLock</strong></a>和<a href="/previous-versions/ff547376(v=vs.85)" data-raw-source="[&lt;strong&gt;WdfInterruptReleaseLock&lt;/strong&gt;](/previous-versions/ff547376(v=vs.85))"><strong>WdfInterruptReleaseLock</strong></a>的调用在 KMDF 回调例程内按平衡方式使用。 在任何 KMDF 回调例程结束时，驱动程序不应持有通过先前对 <strong>WdfInterruptAcquireLock</strong>的调用获取的框架旋转锁对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfspinlock.md" data-raw-source="[&lt;strong&gt;WdfSpinlock&lt;/strong&gt;](kmdf-wdfspinlock.md)"><strong>WdfSpinlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfspinlock.md" data-raw-source="[&lt;strong&gt;WdfSpinlock&lt;/strong&gt;](kmdf-wdfspinlock.md)"><strong>WdfSpinlock</strong></a>规则指定对<a href="/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)" data-raw-source="[&lt;strong&gt;WdfSpinLockAcquire&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))"><strong>WdfSpinLockAcquire</strong></a>方法的调用与<a href="kmdf-wdfspinlockrelease.md" data-raw-source="[&lt;strong&gt;WdfSpinlockRelease&lt;/strong&gt;](kmdf-wdfspinlockrelease.md)"><strong>WdfSpinlockRelease</strong></a>一起用于严格替换。 在任何 KMDF 回调例程结束时，驱动程序不应持有先前对 <strong>WdfSpinLockAcquire</strong>的调用获取的框架旋转锁对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfspinlockrelease.md" data-raw-source="[&lt;strong&gt;WdfSpinlockRelease&lt;/strong&gt;](kmdf-wdfspinlockrelease.md)"><strong>WdfSpinlockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfspinlockrelease.md" data-raw-source="[&lt;strong&gt;WdfSpinlockRelease&lt;/strong&gt;](kmdf-wdfspinlockrelease.md)"><strong>WdfSpinlockRelease</strong></a>规则指定对<a href="/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)" data-raw-source="[&lt;strong&gt;WdfSpinLockAcquire&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))"><strong>WdfSpinLockAcquire</strong></a>和<strong>WdfSpinlockRelease</strong>的调用在 KMDF 事件回调函数内按平衡方式使用。 当 KMDF 事件回调函数返回时，驱动程序不应持有通过先前对 <strong>WdfSpinLockAcquire</strong>的调用获取的框架旋转锁对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-wdfwaitlock.md" data-raw-source="[&lt;strong&gt;WdfWaitlock&lt;/strong&gt;](kmdf-wdfwaitlock.md)"><strong>WdfWaitlock</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfwaitlock.md" data-raw-source="[&lt;strong&gt;WdfWaitlock&lt;/strong&gt;](kmdf-wdfwaitlock.md)"><strong>WdfWaitlock</strong></a>规则指定对<a href="/previous-versions/ff551168(v=vs.85)" data-raw-source="[&lt;strong&gt;WdfWaitLockAcquire&lt;/strong&gt;](/previous-versions/ff551168(v=vs.85))"><strong>WdfWaitLockAcquire</strong></a>的调用用于具有<a href="kmdf-wdfwaitlockrelease.md" data-raw-source="[&lt;strong&gt;WdfWaitlockRelease&lt;/strong&gt;](kmdf-wdfwaitlockrelease.md)"><strong>WdfWaitlockRelease</strong></a>的 strict 替换项。 当 KMDF 事件回调函数返回时，驱动程序不应持有通过先前对 <strong>WdfWaitLockAcquire</strong>的调用获取的框架旋转锁对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-wdfwaitlockrelease.md" data-raw-source="[&lt;strong&gt;WdfWaitlockRelease&lt;/strong&gt;](kmdf-wdfwaitlockrelease.md)"><strong>WdfWaitlockRelease</strong></a></p></td>
<td align="left"><p><a href="kmdf-wdfwaitlockrelease.md" data-raw-source="[&lt;strong&gt;WdfWaitlockRelease&lt;/strong&gt;](kmdf-wdfwaitlockrelease.md)"><strong>WdfWaitlockRelease</strong></a>规则指定对<a href="/previous-versions/ff551168(v=vs.85)" data-raw-source="[&lt;strong&gt;WdfWaitLockAcquire&lt;/strong&gt;](/previous-versions/ff551168(v=vs.85))"><strong>WdfWaitLockAcquire</strong></a>和<a href="/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease" data-raw-source="[&lt;strong&gt;WdfWaitLockRelease&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease)"><strong>WdfWaitlockRelease</strong></a>的调用在 KMDF 事件回调函数内按平衡方式使用。 当 KMDF 事件回调函数返回时，驱动程序不应持有通过先前对 <strong>WdfWaitLockAcquire</strong>的调用获取的框架旋转锁对象。</p></td>
</tr>
</tbody>
</table>

 

**选择锁定规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **锁定**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Locking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

