---
title: 锁定规则集 (NDIS)
description: 使用这些规则来验证您的驱动程序正确管理共享的资源。
ms.assetid: 1123A246-7833-4EAB-B1B8-0C71413CE86B
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: a56edc22dffd1e93b5e1b3aa4653cf0f72280069
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463947"
---
# <a name="locking-rule-set-ndis"></a>锁定规则集 (NDIS)


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
<td align="left"><p><a href="ndis-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](ndis-spinlock.md)"><strong>SpinLock</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](ndis-spinlock.md)"><strong>旋转锁</strong></a>规则验证 NDIS 数值调节钮锁定接口的正确用法。 此规则指定的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff560699" data-raw-source="[&lt;strong&gt;NdisAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560699)"> <strong>NdisAcquireSpinLock</strong> </a>仅旋转锁处于解锁状态时进行。 此规则还会验证微型端口处理程序例程退出之前释放自旋锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-spinlockbalanced.md" data-raw-source="[&lt;strong&gt;SpinLockBalanced&lt;/strong&gt;](ndis-spinlockbalanced.md)"><strong>SpinLockBalanced</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlockbalanced.md" data-raw-source="[&lt;strong&gt;SpinLockBalanced&lt;/strong&gt;](ndis-spinlockbalanced.md)"> <strong>SpinLockBalanced</strong> </a>规则验证获取调节锁的函数的调用的数量是否与发布相同的旋转锁的函数的调用的数相等。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-spinlockdpr.md" data-raw-source="[&lt;strong&gt;SpinLockDpr&lt;/strong&gt;](ndis-spinlockdpr.md)"><strong>SpinLockDpr</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlockdpr.md" data-raw-source="[&lt;strong&gt;SpinLockDpr&lt;/strong&gt;](ndis-spinlockdpr.md)"> <strong>SpinLockDpr</strong> </a>规则验证 NDIS 数值调节钮锁定接口的正确用法。</p>
<p>此规则指定的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff561749" data-raw-source="[&lt;strong&gt;NdisDprAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561749)"> <strong>NdisDprAcquireSpinLock</strong> </a>只有自旋锁处于解锁状态时进行。 此规则还会验证微型端口处理程序例程退出之前释放自旋锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-spinlockdprrelease.md" data-raw-source="[&lt;strong&gt;SpinLockDprRelease&lt;/strong&gt;](ndis-spinlockdprrelease.md)"><strong>SpinLockDprRelease</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlockdprrelease.md" data-raw-source="[&lt;strong&gt;SpinLockDprRelease&lt;/strong&gt;](ndis-spinlockdprrelease.md)"> <strong>SpinLockDprRelease</strong> </a>规则验证的调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff560699" data-raw-source="[&lt;strong&gt;NdisAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560699)"> <strong>NdisAcquireSpinLock</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff561749" data-raw-source="[&lt;strong&gt;NdisDprAcquireSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561749)"> <strong>NdisDprAcquireSpinLock</strong> </a>仅当释放调节锁"解除锁定"状态时调用。 此规则还检查之前退出微型端口处理程序例程旋转锁都已被发布。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinLockRelease&lt;/strong&gt;](ndis-spinlockrelease.md)"><strong>SpinLockRelease</strong></a></p></td>
<td align="left"><p>SpinLockRelease 规则指定一个驱动程序必须释放自旋锁 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff564524" data-raw-source="[&lt;strong&gt;NdisReleaseSpinLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564524)"><strong>NdisReleaseSpinLock</strong></a>) 而不必首先获取它。</p></td>
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

 

 





