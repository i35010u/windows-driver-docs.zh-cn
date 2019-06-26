---
title: RX_CONTEXT 和 IRP 管理
description: RX_CONTEXT 和 IRP 管理
ms.assetid: 74ca681d-2599-442c-aebe-3556d6354f7f
keywords:
- RDBSS WDK 的文件系统 Irp
- 重定向驱动器缓冲子系统 WDK 的文件系统 Irp
- RX_CONTEXT 结构
- 数据结构 WDK 文件系统
- RDBSS WDK 的文件系统、 连接和文件结构
- 重定向驱动器缓冲子系统 WDK 的文件系统、 连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- WDK RDBSS 的连接信息
- Irp WDK RDBSS
- I/O 请求数据包 WDK RDBSS
- 上下文 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 570711bdce506dc3bb1ce06d3903435a3166fa31
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385650"
---
# <a name="rxcontext-and-irp-management"></a>RX\_上下文和 IRP 管理


## <span id="ddk_rx_context_and_irp_management_if"></span><span id="DDK_RX_CONTEXT_AND_IRP_MANAGEMENT_IF"></span>


RX\_上下文结构 RDBSS 所使用的基本数据结构之一，并且网络微型-重定向程序来管理一个 I/O 请求数据包 (IRP)。 RX\_上下文结构描述 IRP，同时它正在处理包含允许为已完成 IRP 释放全局资源的状态信息。 RX\_上下文数据结构封装 IRP 以供 RDBSS，网络微型重定向程序和文件系统。 RX\_上下文结构包含一个指向单个 IRP 和所有处理 IRP 所需的上下文。

RX\_上下文结构有时称为 IRP 上下文或 RxContext Windows Driver Kit (WDK) 标头文件和用于开发网络微型重定向程序驱动程序的其他资源中。

RX\_上下文是由各种网络最小重定向程序提供的其他信息附加到的数据结构。 从设计角度看，可以在以下几种方式处理此附加信息：

-   允许的上下文指针定义为属于 RX\_上下文中，网络微型-重定向程序用于存储离开他们的信息。 这意味着每次 RX\_、 分配和销毁上下文结构网络微型重定向程序驱动程序必须执行单独的关联的分配或包含其他网络的内存块的析构最小重定向程序的信息。 因为 RX\_上下文结构创建和销毁中较大数字，这不是从性能角度来看是可行的解决方案。

-   另一种方法通过分配的每个 RX 大小组成\_上下文结构的每个网络最小重定向器，最小重定向程序然后保留供预先指定的量。 这种方法可避免额外的分配和析构但会增加复杂性 RX\_中 RDBSS 上下文管理代码。

-   第三种方法分配的预先指定的区域，所有网络一部分的每个 RX 的最小重定向程序是相同的包含\_上下文。 这是未格式化的区域之上可以通过各种网络最小重定向程序施加任何所需的结构。 这种方法克服了与以前的方法相关的缺点。 这是当前在 RDBSS 中实现的方法。

第三种方法是使用 RDBSS 的方案。 因此，网络微型重定向程序驱动程序的开发人员应尝试并定义关联的专用上下文而无法容纳到 RX 中定义此预先指定区域\_上下文数据结构。 违反此规则的网络微型重定向程序驱动程序将会产生显著的性能损失。

许多 RDBSS 例程和通过网络微型重定向导出的例程都参考了 RX\_上下文结构或由该例程的一些其他线程中启动线程。 因此，RX\_上下文结构是引用计数，以异步操作的使用进行管理。 当引用计数变为零时，RX\_上下文结构可以完成，并且发布的最后一个取消引用操作。

RDBSS 提供了许多用于操作 RX 的例程的\_上下文结构和相关联的 IRP。 这些例程用于分配、 初始化和删除 RX\_上下文结构。 这些例程还用于完成与 RX IRP\_上下文并设置在取消例程 rx\_上下文。

下面的例程处理 RX\_上下文结构：

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxcompleterequest" data-raw-source="[&lt;strong&gt;RxCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxcompleterequest)"><strong>RxCompleteRequest</strong></a></p></td>
<td align="left"><p>此例程用于完成 IRP 与 RX_CONTEXT 结构相关联。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxcompleterequest_real" data-raw-source="[&lt;strong&gt;RxCompleteRequest_Real&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxcompleterequest_real)"><strong>RxCompleteRequest_Real</strong></a></p></td>
<td align="left"><p>此例程用于完成 IRP 与 RX_CONTEXT 结构相关联。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxcreaterxcontext" data-raw-source="[&lt;strong&gt;RxCreateRxContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxcreaterxcontext)"><strong>RxCreateRxContext</strong></a></p></td>
<td align="left"><p>此例程分配新的 RX_CONTEXT 结构并初始化数据结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real" data-raw-source="[&lt;strong&gt;RxDereferenceAndDeleteRxContext_Real&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real)"><strong>RxDereferenceAndDeleteRxContext_Real</strong></a></p></td>
<td align="left"><p>此例程取消引用一个 RX_CONTEXT 结构和如果引用计数变为零，然后它会解除分配并将删除指定的 RX_CONTEXT 结构从 RDBSS 内存中数据结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxinitializecontext" data-raw-source="[&lt;strong&gt;RxInitializeContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxinitializecontext)"><strong>RxInitializeContext</strong></a></p></td>
<td align="left"><p>此例程初始化新分配的 RX_CONTEXT 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxpreparecontextforreuse" data-raw-source="[&lt;strong&gt;RxPrepareContextForReuse&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxpreparecontextforreuse)"><strong>RxPrepareContextForReuse</strong></a></p></td>
<td align="left"><p>此例程准备 RX_CONTEXT 结构以供重复使用通过重置所有特定于操作的分配和先前所做的收购。 获取从 IRP 的参数不会修改。 此例程 RDBSS 供内部使用和不能由网络微型-重定向程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially" data-raw-source="[&lt;strong&gt;RxResumeBlockedOperations_Serially&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)"><strong>RxResumeBlockedOperations_Serially</strong></a></p></td>
<td align="left"><p>此例程唤醒下一个等待线程，如果有，序列化的阻塞 I/O 队列上。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxsetminirdrcancelroutine" data-raw-source="[&lt;strong&gt;RxSetMinirdrCancelRoutine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-rxsetminirdrcancelroutine)"><strong>RxSetMinirdrCancelRoutine</strong></a></p></td>
<td align="left"><p>例程还设置了网络微型重定向取消 RX_CONTEXT 结构的例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)"><strong>__RxSynchronizeBlockingOperations</strong></a></td>
<td align="left"><p>此例程用于同步到相同的工作队列的阻塞 I/O。 此例程是由在内部用于 RDBSS 同步命名的管道的操作。 此例程可能会通过网络微型重定向，用于同步对单独的队列是由网络微型重定向维护操作。</p>
<p>Windows Server 2003 上才例程。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock)"><strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong></a></td>
<td align="left"><p>此例程用于同步到相同的工作队列的阻塞 I/O。 此例程是由在内部用于 RDBSS 同步命名的管道的操作。 此例程可能会通过网络微型重定向，用于同步对单独的队列是由网络微型重定向维护操作。</p>
<p>Windows XP 和 Windows 2000 上才例程。</p></td>
</tr>
</tbody>
</table>

 

在中定义的以下宏*rxcontx.h*上表中列出调用例程的标头文件。 而不是直接调用这些例程通常使用这些宏。

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
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong>(<em>RXCONTEXT</em>,<em>FCB</em>,<em>IOQUEUE</em>)</p></td>
<td align="left"><p>此宏会同步到相同的工作队列的阻塞 I/O 请求。 在 Windows Server 2003 上此宏将调用<strong>__RxSynchronizeBlockingOperations</strong>例程替换<em>DropFcbLock</em>参数设置为<strong>FALSE</strong>。</p>
<p>在 Windows XP 和 Windows 2000 上，此宏将调用<strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong>例程替换<em>DropFcbLock</em>参数设置为<strong>FALSE</strong>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong>(<em>RXCONTEXT</em>,<em>FCB</em>,<em>IOQUEUE</em>)</p></td>
<td align="left"><p>此宏会同步到相同的工作队列的阻塞 I/O 请求。 在 Windows Server 2003 上此宏将调用<strong>__RxSynchronizeBlockingOperations</strong>例程替换<em>DropFcbLock</em>参数设置为<strong>TRUE</strong>。</p>
<p>在 Windows XP 和 Windows 2000 上，此宏将调用<strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong>例程替换<em>DropFcbLock</em>参数设置为<strong>TRUE</strong>.</p></td>
</tr>
</tbody>
</table>

 

 

 




