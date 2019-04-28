---
title: FCB 资源同步
description: FCB 资源同步
ms.assetid: 8355907e-e313-4e54-a63f-a82d9ce0d31b
keywords:
- RDBSS WDK 的文件系统，FCB 资源同步
- 重定向驱动器缓冲子系统 WDK 的文件系统，FCB 资源同步
- FCB 资源同步 WDK RDBSS
- 分页 I/O WDK RDBSS
- 同步 WDK RDBSS
- 文件控制块结构 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e964fc85743614da56816e66f9348819be860769
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327436"
---
# <a name="fcb-resource-synchronization"></a>FCB 资源同步


## <span id="ddk_fcb_resource_synchronization_if"></span><span id="DDK_FCB_RESOURCE_SYNCHRONIZATION_IF"></span>


最小重定向程序驱动程序感兴趣的同步资源主要与相关联 FCB。 都分页 I/O 资源和常规资源。 分页 I/O 资源由 RDBSS 在内部管理。 最小重定向程序驱动程序可以访问的唯一资源是应使用下面提供的例程访问的常规资源：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553363" data-raw-source="[&lt;strong&gt;RxAcquireExclusiveFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553363)"><strong>RxAcquireExclusiveFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>此例程将获取独占模式下的 FCB 资源。 此例程将等待 FCB 资源之前获取它; 如果免费此例程不返回控件，直到获取独占资源。 此例程获取 FCB 资源，即使已取消与此 FCB 相关联的 RX_CONTEXT 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553372" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553372)"><strong>RxAcquireSharedFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>此例程将获取在共享模式下的 FCB 资源。 此例程将等待要是如果以前以独占方式; 获取免费的 FCB 资源此例程不返回控件，直到获取共享的资源。 此例程获取 FCB 资源，即使已取消与此 FCB 相关联的 RX_CONTEXT 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff553375" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553375)"><strong>RxAcquireSharedFcbResourceInMRxEx</strong></a></td>
<td align="left"><p>此例程将获取在共享模式下的 FCB 资源。 此例程将等待要是如果以前以独占方式; 获取免费的 FCB 资源此例程不返回控件，直到获取共享的资源。 此例程获取 FCB 资源，即使已取消与此 FCB 相关联的 RX_CONTEXT 结构。</p>
<p>Windows Server 2003 Service Pack 1 (SP1) 及更高版本，此例程才可用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff554694" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceForThreadInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554694)"><strong>RxReleaseFcbResourceForThreadInMRx</strong></a></td>
<td align="left"><p>此例程释放以前使用获取的 FCB 资源<a href="https://msdn.microsoft.com/library/windows/hardware/ff553375" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553375)"> <strong>RxAcquireSharedFcbResourceInMRxEx</strong></a>。</p>
<p>此例程才适用于 Windows Server 2003 Service Pack 1 及更高版本。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554699" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554699)"><strong>RxReleaseFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>此例程释放以前使用获取的 FCB 资源<a href="https://msdn.microsoft.com/library/windows/hardware/ff553363" data-raw-source="[&lt;strong&gt;RxAcquireExclusiveFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553363)"> <strong>RxAcquireExclusiveFcbResourceInMRx</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff553372" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553372)"> <strong>RxAcquireSharedFcbResourceInMRx</strong></a>.</p></td>
</tr>
</tbody>
</table>

 

若要确定当前线程是否有权访问 FCB 常规资源 rxprocs.h 标头文件中定义以下宏。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxFcbAcquiredShared</strong> (<em>RXCONTEXT</em>, <em>FCB</em>)</p></td>
<td align="left"><p>此宏检查当前线程是否在共享模式下具有常规资源的访问权限。 此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545477" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545477)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsFcbAcquiredShared</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>此宏检查当前线程是否在共享模式下具有常规资源的访问权限。 此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545477" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545477)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsFcbAcquiredExclusive</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>此宏检查当前线程具有独占模式下对常规资源的访问。 此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545458" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545458)"> <strong>ExIsResourceAcquiredExclusiveLite</strong> </a>例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsFcbAcquired</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>此宏检查当前线程是否在共享或排他模式下具有常规资源的访问权限。 此宏将调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545477" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545477)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff545458" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545458)"> <strong>ExIsResourceAcquiredExclusiveLite</strong> </a>例程。</p></td>
</tr>
</tbody>
</table>

 

 

 




