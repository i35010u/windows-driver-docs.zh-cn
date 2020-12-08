---
title: 工作队列调度机制
description: 工作队列调度机制
keywords:
- RDBSS WDK 文件系统，工作队列调度
- 重定向驱动器缓冲子系统 WDK 文件系统，工作队列调度
- 工作队列调度 WDK RDBSS
- 分派工作队列 WDK RDBSS
- 内存分配 WDK RDBSS
- 关键工作队列 WDK RDBSS
- 延迟的工作队列 WDK RDBSS
- HyperCritical 工作队列 WDK RDBSS
- 簿记 WDK RDBSS
- 统计信息 WDK RDBSS
- 队列 WDK RDBSS
- 状态 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cd27436499de522276d431077b2c35f803f4c20
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816755"
---
# <a name="work-queue-dispatching-mechanisms"></a>工作队列调度机制


## <span id="ddk_work_queue_dispatching_mechanisms_if"></span><span id="DDK_WORK_QUEUE_DISPATCHING_MECHANISMS_IF"></span>


RDBSS 使用 Windows 内核工作队列在多个线程上调度操作以供以后执行。 网络小型重定向器驱动程序可以使用由 RDBSS 维护的工作队列，以供以后执行。

RDBSS 提供了多个例程，用于实现 RDBSS 中使用的调度机制。 这些例程还可以由网络小型重定向程序驱动程序使用。

RDBSS 按设备对象的方式跟踪工作项。 这样，RDBSS 就可以处理与加载和卸载网络微型重定向程序相关的争用条件。 这还提供了 RDBSS 中的一种机制，用于阻止单个网络微型重定向器公平地使用所有资源。

在某些情况下，工作项的分派是不可避免的。 为了避免频繁分配内存和在这些情况下释放操作，会将工作 \_ 队列 \_ 项作为另一个数据的一部分进行分配。 在其他情况下，调度很少发生，这是为了避免在需要时分配内存。 RDBSS 工作队列实现以分派和发布工作队列请求的形式提供这两种方案。 如果使用 [**RxDispatchToWorkerThread**](/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxdispatchtoworkerthread) 例程进行调度，则 \_ 调用方不需要为工作队列 \_ 项分配内存。 若要使用 [**RxPostToWorkerThread**](/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxposttoworkerthread) 例程进行发布，工作队列项的内存必须 \_ \_ 由调用方分配。

向工作线程分派操作的常见情况有两种：

-   对于非常罕见的操作，请使用 **RxDispatchToWorkerThread** 例程来节省内存使用情况，方法是在需要时为工作队列项动态分配和释放内存。

-   当重复调度操作时，请使用 **RxPostToWorkerThread** 例程来节省时间，方法是将工作 \_ 队列 \_ 项作为要调度的数据结构的一部分预先分配。

两次调度操作之间的权衡是时间与空间 (内存使用) 。

RDBSS 中的调度机制以每个处理器为基础提供多个级别的工作队列。 目前支持以下级别的工作队列：

-   严重

-   Delayed

-   HyperCritical

"严重" 和 "延迟" 之间的区别是优先级别之一。 HyperCritical 级别不同于另外两个，因为例程不应阻止 (等待任何资源) 。 此要求不是强制性的，因此，调度机制的有效性取决于客户端的隐式合作。

RDBSS 中的工作队列实现是围绕 KQUEUE 实现构建的。 其他支持包括正在积极等待工作项的多个线程的法规。 每个工作队列数据结构都是从非分页池内存中分配的，并具有自己的同步机制 (旋转锁) 。

除了) 的簿记信息 (队列状态和类型外，RDBSS 还维护在工作队列生存期内收集的统计信息。 这可以提供优化工作队列的宝贵信息。 已处理的项的数目、必须处理的项数以及累积的队列长度为 structureed。 累积队列长度是一个重要的指标，表示每次添加工作项时等待处理的项数之和。 累积队列长度除以处理的项总数和要处理的项的数目，可指示平均队列长度。 如果值大于1，则表示可以增加与工作队列关联的工作线程的最小数目。 值远远小于1表示可以减少与队列关联的最大工作线程数。

工作队列通常在活动状态下启动并继续，直到遇到不可恢复的情况， (缺少系统资源（例如) 或转换为非活动状态时）。 当启动断开时，它将转换为正在进行的状态。

当线程已关闭时，工作队列的断开操作不会完成。 必须先确保线程终止，然后才能关闭数据结构。 RDBSS 中的工作队列实现遵循一个协议，其中每个要旋转的线程都在断开上下文中保存对线程对象的引用。 不属于工作队列 (的 "断开颁发" 线程) 等待在分解数据结构之前已停止的所有线程完成。

**RxDispatchToWorkerThread** 和 **RxPostToWorkerThread** 队列的当前实现工作于发出调用的同一处理器上。

适用于工作队列调度的以下 RDBSS 例程包括。

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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxdispatchtoworkerthread" data-raw-source="[&lt;strong&gt;RxDispatchToWorkerThread&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxdispatchtoworkerthread)"><strong>RxDispatchToWorkerThread</strong></a></p></td>
<td align="left"><p>此例程在工作线程的上下文中调用例程。 此例程分配 WORK_QUEUE_ITEM 的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxposttoworkerthread" data-raw-source="[&lt;strong&gt;RxPostToWorkerThread&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxposttoworkerthread)"><strong>RxPostToWorkerThread</strong></a></p></td>
<td align="left"><p>此例程在工作线程的上下文中调用例程。 WORK_QUEUE_ITEM 的内存必须由调用方分配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxspindownmrxdispatcher" data-raw-source="[&lt;strong&gt;RxSpinDownMRxDispatcher&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxworkq/nf-rxworkq-rxspindownmrxdispatcher)"><strong>RxSpinDownMRxDispatcher</strong></a></p></td>
<td align="left"><p>此例程泪水关闭网络小型重定向程序的调度程序上下文。</p>
<p>请注意，此例程仅适用于 Windows Server 2003 和 Windows XP。</p></td>
</tr>
</tbody>
</table>

 

