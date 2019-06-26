---
title: 驱动程序通知简介
description: 驱动程序通知简介
ms.assetid: c0c09480-628a-4f12-b6a3-881cc3e12fd5
keywords:
- 驱动程序通知 WDK 动态硬件分区、 同步
- 驱动程序通知 WDK 动态硬件分区，异步
- 驱动程序通知 WDK 动态硬件分区内存通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84f08d66871385bf73969b27f7eafbf8dbaedea3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369756"
---
# <a name="introduction-to-driver-notification"></a>驱动程序通知简介

操作系统从 Windows Server 2008 开始，可以通知设备驱动程序的处理器或内存模块时动态添加到硬件分区。 有几个不同的通知发生在不同阶段的过程的一个热添加操作。 这些通知的每个使用不同的通知方法通知设备驱动程序有关的事件。 可以使用一个或多个这些通知方法具有一个热添加操作时通知您的驱动程序的操作系统发生。 然后，您的驱动程序可以响应所需的安全和最佳操作。

下表标识不同的通知方法，无论它们适用于处理器、 内存，或处理器和内存。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>通知方法</th>
<th>处理器</th>
<th>对于内存</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>同步的驱动程序通知</p></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>异步驱动程序通知</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><p>内存通知事件</p></td>
<td></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>重新平衡资源</p></td>
<td><p>X</p></td>
<td></td>
</tr>
</tbody>
</table>

## <a name="synchronous-driver-notification"></a>同步驱动程序通知

与[同步驱动程序通知](synchronous-driver-notification.md)，操作系统以同步方式通知设备驱动程序的新处理器，已添加到硬件分区。 这是第一个设备驱动程序接收有关对处理器的数量的更改的通知。

当新处理器添加到硬件分区时，操作系统将在此通知操作系统已启动新的处理器之后, 但在操作系统开始计划处理器上的线程之前发送到设备驱动程序。 当设备驱动程序收到此通知时，它可以分配每个处理器的任何数据结构，并将任何其他每个处理器资源分配给新的处理器。 这会准备要运行其调度例程，中断服务例程 (Isr) 的设备驱动程序、 延缓的过程调用 (Dpc) 和任何其他驱动程序在新的处理器线程数。

设备驱动程序必须使用操作系统接收同步的驱动程序通知注册自身。 有关详细信息，请参阅[注册同步驱动程序通知](registering-for-synchronous-driver-notification.md)。

此通知方法仅适用于处理器。 内存没有同步的通知机制。

## <a name="asynchronous-driver-notification"></a>异步驱动程序通知

与[异步驱动程序通知](asynchronous-driver-notification.md)，操作系统以异步方式通知设备驱动程序的新的处理器或内存模块，已添加到硬件分区。 从 Windows Server 2008 开始，处理器和内存模块被视为插 (PnP) 设备。 因此，操作系统使用的即插即用通知机制异步驱动程序通知。

当新的处理器或内存模块添加到硬件分区时，操作系统将在此通知操作系统已启动新的处理器或内存设备后发送到设备驱动程序。 对于新的处理器，操作系统不发送此通知设备驱动程序之前已经启动计划新的处理器上的线程。

> [!NOTE]
> 即插即用的所有通知都是异步的。 因此，这些通知可能无法由接收设备驱动程序之前一段时间后在操作系统已启动的处理器或内存模块。

当设备驱动程序收到此通知时，它可以相应地调整某些或所有以下各项：

- 内存缓冲区和其他资源分配

- 与特定处理器的资源的分配

- Dpc 和特定处理器上的其他线程的计划

- 负载平衡算法

> [!IMPORTANT]
> 当将新处理器添加到硬件分区时，操作系统不发送即插即用之前通知后启动新的处理器和操作系统已经开始计划对其线程。 如果设备驱动程序必须执行某些任务，操作系统开始计划新的处理器，如分配的线程之前每个处理器的数据结构，必须为驱动程序使用同步的通知方法。

设备驱动程序必须使用操作系统接收异步驱动程序通知注册自身。 有关详细信息，请参阅[注册为异步的驱动程序通知](registering-for-asynchronous-driver-notification.md)。

## <a name="memory-notification-event"></a>内存通知事件

使用内存通知事件方法，你可以在计划线程等待要设置的操作系统的设备驱动程序 **\\KernelObjects\\HighMemoryCondition**事件对象。 当可用物理内存量超过特定值时，操作系统将设置此事件对象。 此事件通知都在等待该事件的任何线程对象大量物理内存为当前系统中提供。 此事件可能表示动态地向系统添加新内存模块。 在操作系统设置此事件对象，您的设备驱动程序可以响应事件通过分配更多的内存缓冲区。

有关详细信息 **\\KernelObjects\\HighMemoryCondition**事件对象，请参阅[标准事件对象](standard-event-objects.md)。

> [!IMPORTANT]
> 如果操作系统设置 **\\KernelObjects\\HighMemoryCondition**事件对象，该事件仅提供指示，您可能动态地添加了新内存模块的硬件分区。 有可能会导致操作系统来设置此事件对象的其他情形。 因此，从 Windows Server 2008 开始，不建议的设备驱动程序使用此通知方法。 相反，设备驱动程序应使用异步驱动程序通知方法。

此方法仅适用于内存。 没有处理器的相应的通知机制。

## <a name="resource-rebalance"></a>资源重新平衡

从 Windows Server 2008 中，将新处理器添加到硬件分区时，操作系统将启动系统范围资源重新平衡。 设备将参与此类资源重新平衡的设置确定[ **DEVPKEY\_设备\_DHP\_重新平衡\_策略**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-dhp-rebalance-policy)设备的设备属性。 网络适配器中的设备的默认行为 (类 = Net)[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)它们将不参与重新平衡时，新处理器是动态的资源添加到系统。 所有其他设备安装程序类中的设备的默认行为是，它们将参与资源重新平衡新处理器动态添加到系统时。

如果设备是插即用 (PnP) 设备和它参与了此类资源重新平衡，操作系统会发送[ **IRP\_MN\_查询\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)， [ **IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)，并[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device) PnP Irp 到资源重新平衡操作在设备的驱动程序。 这些即插即用请求通知硬件分区中发生了硬件更改的驱动程序。 设备驱动程序应支持通过正确地处理重新平衡资源**IRP\_MN\_查询\_停止\_设备**并**IRP\_MN\_停止\_设备**PnP 请求。 设备驱动程序应永远不会拒绝**IRP\_MN\_查询\_停止\_设备**即插即用的请求。

这些即插即用请求启用设备驱动程序以完全硬件分区中使用一组新的活动处理器后添加新的处理器。 具体而言，支持资源重新平衡的设备驱动程序使用它将接收资源重新平衡，断开其中断服务例程 (Isr)，并将它们与更新后的处理器关联值重新连接期间的即插即用请求。 这样，硬件分区，包括任何新的处理器，用于处理中断请求中使用当前处于活动状态的所有处理器的设备驱动程序。

设备驱动程序应在资源重新平衡期间队列的所有 I/O 请求。

有关资源重新平衡的详细信息，请参阅[停止设备来重新平衡资源](stopping-a-device-to-rebalance-resources.md)。

此方法仅适用于处理器。 将新内存模块添加到硬件分区时，操作系统并不会启动系统范围资源重新平衡。
