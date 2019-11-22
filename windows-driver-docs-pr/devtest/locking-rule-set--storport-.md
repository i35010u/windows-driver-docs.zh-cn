---
title: 锁定规则集 (Storport)
description: 使用这些规则验证驱动程序是否正确管理共享资源。
ms.assetid: FBB75F07-E689-4B7C-B053-E0B6A3772764
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1859aa5c19bfb7fc97c47b933952bf517ba3ab82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840132"
---
# <a name="locking-rule-set-storport"></a>锁定规则集 (Storport)


使用这些规则验证驱动程序是否正确管理共享资源。

## <a name="in-this-section"></a>本部分内容


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
<td align="left"><p><a href="storport-cancelspinlock.md" data-raw-source="[&lt;strong&gt;CancelSpinLock&lt;/strong&gt;](storport-cancelspinlock.md)"><strong>CancelSpinLock</strong></a></p></td>
<td align="left"><p><a href="storport-cancelspinlock.md" data-raw-source="[&lt;strong&gt;CancelSpinLock Rule (Storport)&lt;/strong&gt;](storport-cancelspinlock.md)"><strong>CancelSpinLock 规则（Storport）</strong></a>规则验证对<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)" data-raw-source="[&lt;strong&gt;IoAcquireCancelSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))"><strong>IoAcquireCancelSpinLock</strong></a>的每个调用是否立即后跟对<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)" data-raw-source="[&lt;strong&gt;IoReleaseCancelSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))"><strong>IoReleaseCancelSpinLock</strong></a>的调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](storport-queuedspinlock.md)"><strong>QueuedSpinLock</strong></a></p></td>
<td align="left"><p><a href="storport-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](storport-queuedspinlock.md)"><strong>QueuedSpinLock</strong></a>规则验证如何使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)"><strong>KeReleaseInStackQueuedSpinLock</strong></a>立即释放使用<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLock</strong></a>获取的堆栈内排队自旋锁。 此外，在调度或取消例程结束时，驱动程序不应持有任何锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-queuedspinlockrelease.md" data-raw-source="[&lt;strong&gt;QueuedSpinLockRelease&lt;/strong&gt;](storport-queuedspinlockrelease.md)"><strong>QueuedSpinLockRelease</strong></a></p></td>
<td align="left"><p>此规则验证驱动程序在未首先通过<strong>KeAcquireInStackQueuedSpinLock</strong>获取锁定的情况下不会调用<strong>KeReleaseInStackQueuedSpinLock</strong> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](storport-spinlock.md)"><strong>旋转锁</strong></a></p></td>
<td align="left"><p>此规则验证是否立即调用<strong>KeAcquireSpinLock</strong> ，然后调用<strong>KeReleaseSpinlock</strong>。 如果驱动程序在释放锁之前再次调用<strong>KeAcquireSpinLockRaiseToDpc</strong>或<strong>KeAcquireSpinLock</strong> ，则该规则将失败。 此外，在退出调度或取消例程之前，驱动程序必须释放旋转锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinLockDpc&lt;/strong&gt;](storport-spinlockdpc.md)"><strong>SpinLockDpc</strong></a></p></td>
<td align="left"><p>此规则验证是否立即调用<strong>KeAcquireSpinLockRaiseToDpc</strong> ，然后调用<strong>KeReleaseSpinlock</strong>。 如果驱动程序在释放锁之前再次调用<strong>KeAcquireSpinLock</strong>或<strong>KeAcquireSpinLockRaiseToDpc</strong> ，则该规则将失败。 此外，在退出调度或取消例程之前，驱动程序必须释放旋转锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinLockRelease&lt;/strong&gt;](storport-spinlockrelease.md)"><strong>SpinLockRelease</strong></a></p></td>
<td align="left"><p>此规则验证驱动程序不会尝试通过<strong>KeReleaseSpinLock</strong>释放锁定，无需先通过<strong>KeAquireSpinlock</strong>或<strong>KeAcquireSpinLockRaiseToDpc</strong>获取锁定。 当释放获取的旋转锁时，规则通过。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spinlocksafe.md" data-raw-source="[&lt;strong&gt;SpinLockSafe&lt;/strong&gt;](storport-spinlocksafe.md)"><strong>SpinLockSafe</strong></a></p></td>
<td align="left"><p>此规则验证持有自旋锁时不调用<strong>IoStartNextPacket</strong>和<strong>IoCompleteRequest</strong>例程。 此规则跟踪任何时间持有的旋转锁的数量，如果调用其中一个例程，该数字不是0，则驱动程序将无法满足规则。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportmsilock.md" data-raw-source="[&lt;strong&gt;StorPortMSILock&lt;/strong&gt;](storport-storportmsilock.md)"><strong>StorPortMSILock</strong></a></p></td>
<td align="left"><p>当且仅当<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85)" data-raw-source="[&lt;strong&gt;PORT_CONFIGURATION_INFORMATION (Storport)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))"><strong>PORT_CONFIGURATION_INFORMATION （Storport）</strong></a>结构的<strong>InterruptSynchronizationMode</strong>成员设置为<strong>InterruptSynchronizePerMessage</strong>时，小型端口驱动程序才能获取消息的 MSI 旋转锁。 此规则验证当同步模式为<strong>InterruptSynchronizePerMessage</strong>时，是否仅对<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportacquiremsispinlock" data-raw-source="[&lt;strong&gt;StorPortAcquireMSISpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportacquiremsispinlock)"><strong>StorPortAcquireMSISpinLock</strong></a>进行调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportspinlock.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock&lt;/strong&gt;](storport-storportspinlock.md)"><strong>StorPortSpinLock</strong></a></p></td>
<td align="left"><p>此规则验证通过 StorPortReleaseSpinLock 获取的<strong>锁定是否立即通过</strong>发布。 如果小型小型驱动程序尝试获取已获取的锁定，或者尝试释放尚未获取的锁定，则该规则将无法使用该规则。 此外，在调度或取消例程结束时，驱动程序不应持有任何自旋锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportspinlock3.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock3&lt;/strong&gt;](storport-storportspinlock3.md)"><strong>StorPortSpinLock3</strong></a></p></td>
<td align="left"><p><a href="storport-storportspinlock3.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock3&lt;/strong&gt;](storport-storportspinlock3.md)"><strong>StorPortSpinLock3</strong></a>规则验证<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportacquirespinlock" data-raw-source="[&lt;strong&gt;StorPortAcquireSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportacquirespinlock)"><strong>StorPortAcquireSpinLock</strong></a>例程的文档中描述的锁获取层次结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportspinlock4.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock4&lt;/strong&gt;](storport-storportspinlock4.md)"><strong>StorPortSpinLock4</strong></a></p></td>
<td align="left"><p>此规则是<strong>StorPortSpinLock</strong>的对应<em>发布</em>。 它类似于<strong>SpinLockRelease</strong>规则。</p></td>
</tr>
</tbody>
</table>

 

**选择锁定规则集**

1.  在 Microsoft Visual Studio 中选择驱动程序项目（. .Vcxproj）。 在 "**驱动程序**" 菜单中，单击 "**启动静态驱动程序验证程序 ...** "。

2.  单击 "**规则**" 选项卡。在 "**规则集**" 下，选择 "**锁定**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check**选项指定**sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Locking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[使用静态驱动程序验证器查找驱动程序中的缺陷](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)和[静态驱动程序验证程序命令（MSBuild）](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





