---
title: 调度机制的工作队列
description: 调度机制的工作队列
ms.assetid: d4ce929f-2d84-4194-9afa-e00629594c36
keywords:
- RDBSS WDK 文件系统是如何工作队列调度
- 重定向驱动器缓冲子系统 WDK 文件系统是如何工作队列调度
- 调度 WDK RDBSS 工作队列
- 调度工作队列 WDK RDBSS
- 内存分配 WDK RDBSS
- 关键的工作队列 WDK RDBSS
- 延迟工作队列 WDK RDBSS
- HyperCritical 工作队列 WDK RDBSS
- WDK RDBSS 簿记
- WDK RDBSS 的统计信息
- 队列 WDK RDBSS
- 指出 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 048e3de725fe96da64cc97e96bf208aa49cc6d5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519102"
---
# <a name="work-queue-dispatching-mechanisms"></a>调度机制的工作队列


## <span id="ddk_work_queue_dispatching_mechanisms_if"></span><span id="DDK_WORK_QUEUE_DISPATCHING_MECHANISMS_IF"></span>


RDBSS 使用 Windows 内核工作队列中调度多个线程上供以后执行的操作。 网络微型重定向程序驱动程序可以使用由 RDBSS 维护对调度操作的更高版本执行的工作队列。

RDBSS 提供了几个在 RDBSS 中实现时使用的调度机制的例程。 网络微型重定向程序驱动程序还可以使用这些例程。

在每个设备对象的基础上的工作项跟踪的 RDBSS。 这允许 RDBSS 来处理与加载和卸载网络微型-重定向程序关联的争用条件。 这还提供了一种机制中 RDBSS 防止单个网络微型重定向不公平地使用的所有资源。

有哪些调度的工作项是不可避免地存在某些方案。 若要避免频繁的内存分配和释放操作在这些情况下，工作\_队列\_项分配作为另一个数据的一部分。 在其中调度是极少数其他情况下，它物有所值以避免内存分配，除非必需。 RDBSS 工作队列实现为这两个方案中调度和发布工作队列请求的形式提供。 在调度使用的情况下[ **RxDispatchToWorkerThread** ](https://msdn.microsoft.com/library/windows/hardware/ff554398)例程，没有内存的工作\_队列\_需要由调用方分配的项。 用于发布使用[ **RxPostToWorkerThread** ](https://msdn.microsoft.com/library/windows/hardware/ff554620)例程的工作内存\_队列\_需要由调用方分配的项。

有两种常见情况的工作线程的调度操作：

-   对于很少发生的操作，使用**RxDispatchToWorkerThread**例程，以通过动态分配和释放内存的工作队列项在需要时，从而节省内存使用。

-   当某个操作将重复进行调度时，使用**RxPostToWorkerThread**例程，以通过预先分配工作，从而节省时间\_队列\_作为数据结构的一部分的项以进行调度.

两个调度操作之间一优势是与空间 （内存使用） 的时间。

RDBSS 中的调度机制提供的多个级别的每个处理器进行的工作队列。 工作队列中当前支持以下级别：

-   严重

-   延迟

-   HyperCritical

严重和延迟之间的区别是一个优先级。 HyperCritical 级别的与其他两个不同在于例程不应阻塞 （等待任何资源）。 不能强制实施此要求，因此调度机制的有效性依赖于客户端的隐式协作。

围绕 KQUEUE 实现构建 RDBSS 中的工作队列实现。 其他支持涉及条例的主动等待工作项的线程数。 每个工作队列数据结构从非分页缓冲的池内存分配，并具有其自己的同步机制 （自旋锁）。

除了簿记信息 （队列状态和类型，例如），RDBSS 还维护工作队列的生存期内收集的统计信息。 这可以提供优化的工作队列中有价值的信息。 已处理的项数，项的数目，需要进行处理，并累积的队列长度是 structureed。 累积的队列长度是重要的指标，表示等待处理每个额外的工作项已排入队列的时间的项的数目之和。 处理的总项数和要处理的项目数的总和除以累积的队列长度给出平均队列长度的指示。 更多个值表示可以增加的最小工作队列与关联的工作线程数。 值太多不会早于一个表示可减少最大与队列关联的工作线程数。

工作队列通常启动处于活动状态，并继续之前的非可恢复情况下遇到 （缺乏系统资源，例如） 或当它将转换为非活动状态。 启动断开时，它将转换为正在断开状态。

当线程具有降速时，才会完成的工作队列断开。 需要的数据结构可关闭之前确保线程终止。 RDBSS 中的工作队列实现都遵循的协议在其中每个休眠线程将保存到断开的上下文中的线程对象的引用。 发出线程 （以及不属于工作队列） 断开等待完成的所有线程盘片降速之前关闭的数据结构。

当前实现**RxDispatchToWorkerThread**并**RxPostToWorkerThread**到发起调用的同一个处理器上将工作排队。

包括以下 RDBSS 例程用于调度工作队列。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554398" data-raw-source="[&lt;strong&gt;RxDispatchToWorkerThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554398)"><strong>RxDispatchToWorkerThread</strong></a></p></td>
<td align="left"><p>此例程调用的工作线程的上下文中的例程。 此例程分配了 WORK_QUEUE_ITEM 的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554620" data-raw-source="[&lt;strong&gt;RxPostToWorkerThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554620)"><strong>RxPostToWorkerThread</strong></a></p></td>
<td align="left"><p>此例程调用的工作线程的上下文中的例程。 必须由调用方分配 WORK_QUEUE_ITEM 内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554734" data-raw-source="[&lt;strong&gt;RxSpinDownMRxDispatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554734)"><strong>RxSpinDownMRxDispatcher</strong></a></p></td>
<td align="left"><p>此例程卸除网络微型重定向的调度程序上下文。</p>
<p>请注意，此例程仅可在 Windows Server 2003 和 Windows XP 上。</p></td>
</tr>
</tbody>
</table>

 

 

 




