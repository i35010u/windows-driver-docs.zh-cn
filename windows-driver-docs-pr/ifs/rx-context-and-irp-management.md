---
title: RX_CONTEXT 和 IRP 管理
description: RX_CONTEXT 和 IRP 管理
keywords:
- RDBSS WDK 文件系统，Irp
- 重定向驱动器缓冲子系统 WDK 文件系统、Irp
- RX_CONTEXT 结构
- 数据结构 WDK 文件系统
- RDBSS WDK 文件系统、连接和文件结构
- 重定向的驱动器缓冲子系统 WDK 文件系统、连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- 连接信息 WDK RDBSS
- Irp WDK RDBSS
- I/o 请求数据包 WDK RDBSS
- 上下文 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a39472744a655dc7a29cda303242c9467fa5323b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789923"
---
# <a name="rx_context-and-irp-management"></a>RX \_ 上下文和 IRP 管理


## <span id="ddk_rx_context_and_irp_management_if"></span><span id="DDK_RX_CONTEXT_AND_IRP_MANAGEMENT_IF"></span>


RX \_ 上下文结构是 RDBSS 和网络微型重定向程序用来管理 i/o 请求数据包 (IRP) 的基本数据结构之一。 RX \_ 上下文结构描述正在处理的 IRP，并包含允许在完成 IRP 后释放全局资源的状态信息。 RX \_ 上下文数据结构封装了用于 RDBSS、网络微型重定向程序和文件系统的 IRP。 RX \_ 上下文结构包含指向单个 IRP 和处理 IRP 所需的所有上下文的指针。

\_在 Windows 驱动程序工具包中，RX 上下文结构有时称为 IRP 上下文或 RxContext， (WDK) 头文件和用于开发网络小型重定向程序驱动程序的其他资源。

RX \_ 上下文是一种数据结构，其附加信息由各种网络微型重定向程序提供。 从设计的角度来看，可以通过以下几种方式之一来处理此附加信息：

-   允许将上下文指针定义为 RX 上下文的一部分 \_ ，网络小型重定向器使用该上下文来存储信息。 这意味着，每次 \_ 分配和销毁 RX 上下文结构时，网络微型重定向程序驱动程序都必须执行单独关联的内存块分配或销毁，其中包含额外的网络微型重定向程序信息。 由于 RX \_ 上下文结构的创建和销毁数量很大，因此从性能角度来看，这并不是可接受的解决方案。

-   另一种方法是将每个 RX 上下文结构的大小分配 \_ 给每个网络微型重定向程序的预先指定的量，然后将其保留供微型重定向程序使用。 这种方法可避免额外的分配和析构，但会使 \_ RDBSS 中的 RX 上下文管理代码变得更加复杂。

-   第三种方法包括分配预先指定的区域，该区域对于所有网络微型重定向程序都是相同的，作为每个 RX 上下文的一部分 \_ 。 这是一个未格式化的区域，其中的所有所需结构都可由各种网络微型重定向器施加。 这种方法克服了与先前方法关联的缺点。 这是当前在 RDBSS 中实现的方法。

第三种方法是 RDBSS 使用的方案。 因此，网络小型重定向程序驱动程序的开发人员应尝试并定义关联的私有上下文，使其适合在 RX 上下文数据结构中定义的此预先指定的区域 \_ 。 违反此规则的网络微重定向程序驱动程序将导致严重的性能损失。

许多由网络微型重定向程序导出的 RDBSS 例程和例程在 \_ 启动线程中或例程使用的其他线程中引用 RX 上下文结构。 因此，RX \_ 上下文结构是引用计数的，以管理它们对异步操作的使用。 当引用计数变为零时，RX \_ 上下文结构可以在最后一个取消引用操作上完成和释放。

RDBSS 提供了许多用于处理 RX \_ 上下文结构和关联的 IRP 的例程。 这些例程用于分配、初始化和删除 RX \_ 上下文结构。 这些例程还用于完成与 RX 上下文关联的 IRP \_ ，并为 rx 上下文设置取消例程 \_ 。

以下例程操作 RX \_ 上下文结构：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest" data-raw-source="[&lt;strong&gt;RxCompleteRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest)"><strong>RxCompleteRequest</strong></a></p></td>
<td align="left"><p>此例程用于完成与 RX_CONTEXT 结构关联的 IRP。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest_real" data-raw-source="[&lt;strong&gt;RxCompleteRequest_Real&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxcompleterequest_real)"><strong>RxCompleteRequest_Real</strong></a></p></td>
<td align="left"><p>此例程用于完成与 RX_CONTEXT 结构关联的 IRP。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxcreaterxcontext" data-raw-source="[&lt;strong&gt;RxCreateRxContext&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxcreaterxcontext)"><strong>RxCreateRxContext</strong></a></p></td>
<td align="left"><p>此例程分配新的 RX_CONTEXT 结构并初始化数据结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real" data-raw-source="[&lt;strong&gt;RxDereferenceAndDeleteRxContext_Real&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxdereferenceanddeleterxcontext_real)"><strong>RxDereferenceAndDeleteRxContext_Real</strong></a></p></td>
<td align="left"><p>此例程取消引用 RX_CONTEXT 的结构，如果引用计数变为零，则它会从 RDBSS 内存中数据结构释放并删除指定的 RX_CONTEXT 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxinitializecontext" data-raw-source="[&lt;strong&gt;RxInitializeContext&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxinitializecontext)"><strong>RxInitializeContext</strong></a></p></td>
<td align="left"><p>此例程初始化新分配的 RX_CONTEXT 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxpreparecontextforreuse" data-raw-source="[&lt;strong&gt;RxPrepareContextForReuse&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxpreparecontextforreuse)"><strong>RxPrepareContextForReuse</strong></a></p></td>
<td align="left"><p>此例程通过重置所有特定于操作的分配和之前进行的购置，来准备 RX_CONTEXT 结构以供重用。 不会修改从 IRP 获取的参数。 此例程由 RDBSS 在内部使用，不应由网络微型重定向程序使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially" data-raw-source="[&lt;strong&gt;RxResumeBlockedOperations_Serially&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxresumeblockedoperations_serially)"><strong>RxResumeBlockedOperations_Serially</strong></a></p></td>
<td align="left"><p>此例程唤醒序列化阻塞 i/o 队列上的下一个等待线程（如果有）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxsetminirdrcancelroutine" data-raw-source="[&lt;strong&gt;RxSetMinirdrCancelRoutine&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-rxsetminirdrcancelroutine)"><strong>RxSetMinirdrCancelRoutine</strong></a></p></td>
<td align="left"><p>例程为 RX_CONTEXT 结构设置网络小型重定向器取消例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)"><strong>__RxSynchronizeBlockingOperations</strong></a></td>
<td align="left"><p>此例程用于将阻塞的 i/o 同步到相同的工作队列。 此例程由 RDBSS 在内部使用，用于同步命名管道操作。 网络小型重定向程序可能会使用此例程来同步网络小型重定向程序维护的单独队列上的操作。</p>
<p>例程只能在 Windows Server 2003 上使用。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](./--rxsynchronizeblockingoperationsmaybedroppingfcblock.md)"><strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong></a></td>
<td align="left"><p>此例程用于将阻塞的 i/o 同步到相同的工作队列。 此例程由 RDBSS 在内部使用，用于同步命名管道操作。 网络小型重定向程序可能会使用此例程来同步网络小型重定向程序维护的单独队列上的操作。</p>
<p>例程只能在 Windows XP 和 Windows 2000 上使用。</p></td>
</tr>
</tbody>
</table>

 

以下宏在 *rxcontx* 头文件中定义，该文件调用上表中列出的例程。 通常使用这些宏，而不是直接调用这些例程。

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
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong> (<em>RXCONTEXT</em>、<em>FCB</em>、<em>IOQUEUE</em>) </p></td>
<td align="left"><p>此宏将阻塞 i/o 请求同步到相同的工作队列。 在 Windows Server 2003 上，此宏调用 <strong>__RxSynchronizeBlockingOperations</strong> 例程，并将 <em>DropFcbLock</em> 参数设置为 <strong>FALSE</strong>。</p>
<p>在 Windows XP 和 Windows 2000 上，此宏会调用 <strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong> 例程，并将 <em>DropFcbLock</em> 参数设置为 <strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong> (<em>RXCONTEXT</em>、<em>FCB</em>、<em>IOQUEUE</em>) </p></td>
<td align="left"><p>此宏将阻塞 i/o 请求同步到相同的工作队列。 在 Windows Server 2003 上，此宏调用 <strong>__RxSynchronizeBlockingOperations</strong> 例程，并将 <em>DropFcbLock</em> 参数设置为 <strong>TRUE</strong>。</p>
<p>在 Windows XP 和 Windows 2000 上，此宏会调用 <strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong> 例程，并将 <em>DropFcbLock</em> 参数设置为 <strong>TRUE</strong>。</p></td>
</tr>
</tbody>
</table>

 

