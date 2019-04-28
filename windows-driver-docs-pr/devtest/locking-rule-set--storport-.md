---
title: 锁定规则集 (Storport)
description: 使用这些规则来验证您的驱动程序正确管理共享的资源。
ms.assetid: FBB75F07-E689-4B7C-B053-E0B6A3772764
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 38de63d1770270d1b458c3c1c73d48819c77f5a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352887"
---
# <a name="locking-rule-set-storport"></a>锁定规则集 (Storport)


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
<td align="left"><p><a href="storport-cancelspinlock.md" data-raw-source="[&lt;strong&gt;CancelSpinLock&lt;/strong&gt;](storport-cancelspinlock.md)"><strong>CancelSpinLock</strong></a></p></td>
<td align="left"><p><a href="storport-cancelspinlock.md" data-raw-source="[&lt;strong&gt;CancelSpinLock Rule (Storport)&lt;/strong&gt;](storport-cancelspinlock.md)"> <strong>CancelSpinLock 规则 (Storport)</strong> </a>规则验证每次调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548196" data-raw-source="[&lt;strong&gt;IoAcquireCancelSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548196)"> <strong>IoAcquireCancelSpinLock</strong> </a>及时跟调用到<a href="https://msdn.microsoft.com/library/windows/hardware/ff549550" data-raw-source="[&lt;strong&gt;IoReleaseCancelSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549550)"> <strong>IoReleaseCancelSpinLock</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](storport-queuedspinlock.md)"><strong>QueuedSpinLock</strong></a></p></td>
<td align="left"><p><a href="storport-queuedspinlock.md" data-raw-source="[&lt;strong&gt;QueuedSpinLock&lt;/strong&gt;](storport-queuedspinlock.md)"> <strong>QueuedSpinLock</strong> </a>规则验证该堆栈中的-排入队列使用获取的自旋锁<a href="https://msdn.microsoft.com/library/windows/hardware/ff551899" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551899)"> <strong>KeAcquireInStackQueuedSpinLock</strong> </a>会立即释放使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff553130" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553130)"> <strong>KeReleaseInStackQueuedSpinLock</strong></a>。 此外，在调度或取消例程结束时，该驱动程序应该不占用任何锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-queuedspinlockrelease.md" data-raw-source="[&lt;strong&gt;QueuedSpinLockRelease&lt;/strong&gt;](storport-queuedspinlockrelease.md)"><strong>QueuedSpinLockRelease</strong></a></p></td>
<td align="left"><p>此规则将验证该驱动程序不会调用<strong>KeReleaseInStackQueuedSpinLock</strong>而不必首先获取通过锁<strong>KeAcquireInStackQueuedSpinLock</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](storport-spinlock.md)"><strong>SpinLock</strong></a></p></td>
<td align="left"><p>此规则验证调用<strong>KeAcquireSpinLock</strong>及时跟调用<strong>KeReleaseSpinlock</strong>。 如果驱动程序调用<strong>KeAcquireSpinLockRaiseToDpc</strong>或<strong>KeAcquireSpinLock</strong>再次释放锁之前, 失败的规则。 此外之前退出调度或取消例程，该驱动程序必须释放自旋锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spinlockdpc.md" data-raw-source="[&lt;strong&gt;SpinLockDpc&lt;/strong&gt;](storport-spinlockdpc.md)"><strong>SpinLockDpc</strong></a></p></td>
<td align="left"><p>此规则验证调用<strong>KeAcquireSpinLockRaiseToDpc</strong>及时跟调用<strong>KeReleaseSpinlock</strong>。 如果驱动程序调用<strong>KeAcquireSpinLock</strong>或<strong>KeAcquireSpinLockRaiseToDpc</strong>再次释放锁之前, 失败的规则。 此外之前退出调度或取消例程，该驱动程序必须释放自旋锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinLockRelease&lt;/strong&gt;](storport-spinlockrelease.md)"><strong>SpinLockRelease</strong></a></p></td>
<td align="left"><p>此规则将验证该驱动程序不会尝试释放通过锁<strong>KeReleaseSpinLock</strong>而不必首先获取通过<strong>KeAquireSpinlock</strong>或<strong>KeAcquireSpinLockRaiseToDpc</strong>. 获取数值调节钮锁被释放时，将传递规则。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spinlocksafe.md" data-raw-source="[&lt;strong&gt;SpinLockSafe&lt;/strong&gt;](storport-spinlocksafe.md)"><strong>SpinLockSafe</strong></a></p></td>
<td align="left"><p>此规则验证<strong>IoStartNextPacket</strong>并<strong>IoCompleteRequest</strong>例程不会占用自旋锁时调用。 规则跟踪的数值调节钮持有的锁数量在任何时候，如果该数字不是 0 时调用任一例程时，该驱动程序未能通过该规则。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportmsilock.md" data-raw-source="[&lt;strong&gt;StorPortMSILock&lt;/strong&gt;](storport-storportmsilock.md)"><strong>StorPortMSILock</strong></a></p></td>
<td align="left"><p>微型端口驱动程序所需，当且仅当，获取一条消息的 MSI 数值调节钮锁定<strong>InterruptSynchronizationMode</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff563901" data-raw-source="[&lt;strong&gt;PORT_CONFIGURATION_INFORMATION (Storport)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563901)"> <strong>PORT_CONFIGURATION_INFORMATION (Storport)</strong></a>结构设置为<strong>InterruptSynchronizePerMessage</strong>。 此规则验证的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567023" data-raw-source="[&lt;strong&gt;StorPortAcquireMSISpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567023)"> <strong>StorPortAcquireMSISpinLock</strong> </a>如果同步模式，则仅进行<strong>InterruptSynchronizePerMessage</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportspinlock.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock&lt;/strong&gt;](storport-storportspinlock.md)"><strong>StorPortSpinLock</strong></a></p></td>
<td align="left"><p>此规则验证的锁的通过获取<strong>StorPortAcquireSpinLock</strong>立即释放通过<strong>StorPortReleaseSpinLock</strong>。 如果它尝试获取锁，已获得它，或如果它尝试发布具有未获取的锁将微型端口驱动程序失败规则。 此外，在调度或取消例程结束时，该驱动程序不应阻止任何自旋锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportspinlock3.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock3&lt;/strong&gt;](storport-storportspinlock3.md)"><strong>StorPortSpinLock3</strong></a></p></td>
<td align="left"><p><a href="storport-storportspinlock3.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock3&lt;/strong&gt;](storport-storportspinlock3.md)"> <strong>StorPortSpinLock3</strong> </a>规则验证的文档中所述在锁获取层次结构<a href="https://msdn.microsoft.com/library/windows/hardware/ff567025" data-raw-source="[&lt;strong&gt;StorPortAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567025)"> <strong>StorPortAcquireSpinLock</strong></a>例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportspinlock4.md" data-raw-source="[&lt;strong&gt;StorPortSpinLock4&lt;/strong&gt;](storport-storportspinlock4.md)"><strong>StorPortSpinLock4</strong></a></p></td>
<td align="left"><p>此规则<em>释放</em>的对应<strong>StorPortSpinLock</strong>。 它是类似于<strong>SpinLockRelease</strong>规则。</p></td>
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

 

 





