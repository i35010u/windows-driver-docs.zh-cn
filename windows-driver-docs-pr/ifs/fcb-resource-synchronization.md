---
title: FCB 资源同步
description: FCB 资源同步
ms.assetid: 8355907e-e313-4e54-a63f-a82d9ce0d31b
keywords:
- RDBSS WDK 文件系统，FCB 资源同步
- 重定向驱动器缓冲子系统 WDK 文件系统，FCB 资源同步
- FCB 资源同步 WDK RDBSS
- 分页 i/o WDK RDBSS
- 同步 WDK RDBSS
- 文件控制块结构 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 727fcff62790ba397bdee145bf1840764558bf87
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063688"
---
# <a name="fcb-resource-synchronization"></a>FCB 资源同步


## <span id="ddk_fcb_resource_synchronization_if"></span><span id="DDK_FCB_RESOURCE_SYNCHRONIZATION_IF"></span>


最小重定向程序驱动程序所需的同步资源主要与 FCB 关联。 存在分页 i/o 资源和常规资源。 分页 i/o 资源由 RDBSS 在内部进行管理。 最小化重定向程序驱动程序可访问的唯一资源是常规资源，应使用以下提供的例程访问该资源：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireExclusiveFcbResourceInMRx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx)"><strong>RxAcquireExclusiveFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>此例程获取独占模式下的 FCB 资源。 如果之前已获取 FCB 资源，此例程将等待该资源空闲;在获取独占资源之前，此例程不会返回控制。 即使已取消与此 FCB 关联的 RX_CONTEXT 结构，此例程也会获取 FCB 资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx)"><strong>RxAcquireSharedFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>此例程获取共享模式下的 FCB 资源。 如果以前以独占方式获取 FCB 资源，此例程将等待该资源空闲;在获取共享资源之前，此例程不会返回控制。 即使已取消与此 FCB 关联的 RX_CONTEXT 结构，此例程也会获取 FCB 资源。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex)"><strong>RxAcquireSharedFcbResourceInMRxEx</strong></a></td>
<td align="left"><p>此例程获取共享模式下的 FCB 资源。 如果以前以独占方式获取 FCB 资源，此例程将等待该资源空闲;在获取共享资源之前，此例程不会返回控制。 即使已取消与此 FCB 关联的 RX_CONTEXT 结构，此例程也会获取 FCB 资源。</p>
<p>此例程仅在 Windows Server 2003 Service Pack 1 (SP1) 和更高版本上可用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceForThreadInMRx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)"><strong>RxReleaseFcbResourceForThreadInMRx</strong></a></td>
<td align="left"><p>此例程释放以前使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex)"><strong>RxAcquireSharedFcbResourceInMRxEx</strong></a>获取的 FCB 资源。</p>
<p>此例程仅在 Windows Server 2003 Service Pack 1 和更高版本上可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceInMRx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceinmrx)"><strong>RxReleaseFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>此例程释放以前使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireExclusiveFcbResourceInMRx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx)"><strong>RxAcquireExclusiveFcbResourceInMRx</strong></a> 或 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRx&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx)"><strong>RXACQUIRESHAREDFCBRESOURCEINMRX</strong></a>获取的 FCB 资源。</p></td>
</tr>
</tbody>
</table>

 

以下宏在 rxprocs 头文件中定义，以确定当前线程是否有权访问 FCB 常规资源。

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
<td align="left"><p><strong>RxFcbAcquiredShared</strong> (<em>RXCONTEXT</em>， <em>FCB</em>) </p></td>
<td align="left"><p>此宏检查当前线程是否有权访问共享模式下的常规资源。 此宏调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a> 例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsFcbAcquiredShared</strong> (<em>FCB</em>) </p></td>
<td align="left"><p>此宏检查当前线程是否有权访问共享模式下的常规资源。 此宏调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a> 例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsFcbAcquiredExclusive</strong> (<em>FCB</em>) </p></td>
<td align="left"><p>此宏检查当前线程是否有权访问独占模式下的常规资源。 此宏调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)"><strong>ExIsResourceAcquiredExclusiveLite</strong></a> 例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsFcbAcquired</strong> (<em>FCB</em>) </p></td>
<td align="left"><p>此宏检查当前线程是否有权访问共享或独占模式下的常规资源。 此宏将调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a> 和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)"><strong>ExIsResourceAcquiredExclusiveLite</strong></a> 例程。</p></td>
</tr>
</tbody>
</table>

 

 

