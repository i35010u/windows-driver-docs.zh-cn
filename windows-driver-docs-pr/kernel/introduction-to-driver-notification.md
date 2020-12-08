---
title: 驱动程序通知简介
description: 驱动程序通知简介
keywords:
- 驱动程序通知 WDK 动态硬件分区，同步
- 驱动程序通知 WDK 动态硬件分区，异步
- 驱动程序通知 WDK 动态硬件分区，内存通知
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d474fa3eafb1cf108a5fd2b0b76f23a22c4b04b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837239"
---
# <a name="introduction-to-driver-notification"></a>驱动程序通知简介

从 Windows Server 2008 开始，当处理器或内存模块动态添加到硬件分区时，操作系统可以通知设备驱动程序。 热添加操作过程的不同阶段发生了几个不同的通知。 其中每个通知都使用不同的通知方法，通知设备驱动程序事件。 当热添加操作发生时，可以使用这些通知方法中的一个或多个来使操作系统通知驱动程序。 然后，你的驱动程序可以根据需要对安全和最佳操作做出响应。

下表列出了不同的通知方法，以及它们是适用于处理器、内存还是同时适用于处理器和内存。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>通知方法</th>
<th>处理器的</th>
<th>对于内存</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>同步驱动程序通知</p></td>
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
<td><p>资源重新平衡</p></td>
<td><p>X</p></td>
<td></td>
</tr>
</tbody>
</table>

## <a name="synchronous-driver-notification"></a>同步驱动程序通知

使用 [同步驱动程序通知](registering-for-synchronous-driver-notification.md)时，操作系统将同步通知设备驱动程序已将新处理器添加到硬件分区。 这是设备驱动程序收到的有关处理器数量变化的第一个通知。

将新处理器添加到硬件分区后，操作系统会在操作系统启动新处理器后，但在操作系统开始计划处理器上的线程之前，将此通知发送到设备驱动程序。 当设备驱动程序收到此通知时，它可以分配任何每个处理器的数据结构，并将任何其他每个处理器资源分配给新的处理器。 这将准备设备驱动程序以运行其调度例程，中断服务例程 (Isr) ，延迟的过程调用 (Dpc) ，以及新处理器上的任何其他驱动程序线程。

设备驱动程序必须向操作系统注册自身，才能接收同步驱动程序通知。 有关详细信息，请参阅 [注册同步驱动程序通知](registering-for-synchronous-driver-notification.md)。

此通知方法仅适用于处理器。 内存没有同步通知机制。

## <a name="asynchronous-driver-notification"></a>异步驱动程序通知

使用 [异步驱动程序通知](registering-for-asynchronous-driver-notification.md)，操作系统会以异步方式通知设备驱动程序，新处理器或内存模块已添加到硬件分区。 从 Windows Server 2008 开始，会将处理器和内存模块视为即插即用 (PnP) 设备。 因此，操作系统使用用于异步驱动程序通知的 PnP 通知机制。

将新处理器或内存模块添加到硬件分区时，操作系统启动了新的处理器或内存设备后，操作系统会将此通知发送到设备驱动程序。 对于新的处理器，操作系统不会将此通知发送到设备驱动程序，直到开始在新处理器上计划线程为止。

> [!NOTE]
> 所有 PnP 通知都是异步的。 因此，在操作系统启动处理器或内存模块之后，设备驱动程序可能无法接收这些通知。

当设备驱动程序收到此通知时，它可以相应地调整部分或全部以下项：

- 内存缓冲区和其他资源分配

- 将资源分配给特定处理器

- 在特定处理器上计划 Dpc 和其他线程

- 负载平衡算法

> [!IMPORTANT]
> 将新处理器添加到硬件分区时，操作系统将不会发送 PnP 通知，直到启动新的处理器，并且操作系统已开始为其计划线程。 如果设备驱动程序必须在操作系统开始计划新处理器上的线程之前执行某些任务（例如分配每个处理器的数据结构），则必须为驱动程序使用同步通知方法。

设备驱动程序必须向操作系统注册自身，才能接收异步驱动程序通知。 有关详细信息，请参阅 [注册异步驱动程序通知](registering-for-asynchronous-driver-notification.md)。

## <a name="memory-notification-event"></a>内存通知事件

使用内存通知事件方法，你可以让设备驱动程序安排一个线程，该线程等待操作系统设置 **\\ KernelObjects \\ HighMemoryCondition** 事件对象。 当可用物理内存量超过特定值时，操作系统将设置此事件对象。 此事件通知正在等待事件对象的所有线程当前在系统中可用的物理内存量。 此事件可能表示您动态向系统中添加了一个新的内存模块。 当操作系统设置此事件对象时，您的设备驱动程序可以通过分配更多的内存缓冲区来响应事件。

有关 **\\ KernelObjects \\ HighMemoryCondition** 事件对象的详细信息，请参阅 [标准事件对象](standard-event-objects.md)。

> [!IMPORTANT]
> 如果操作系统设置 **\\ KernelObjects \\ HighMemoryCondition** 事件对象，则该事件只会指示您可能已将新内存模块动态添加到硬件分区。 在其他情况下，可能会导致操作系统设置此事件对象。 因此，从 Windows Server 2008 开始，我们不建议设备驱动程序使用此通知方法。 设备驱动程序应使用异步驱动程序通知方法。

此方法仅适用于内存。 处理器没有相应的通知机制。

## <a name="resource-rebalance"></a>资源重新平衡

从 Windows Server 2008 开始，当你将新处理器添加到硬件分区时，操作系统将启动系统范围内的资源重新平衡。 设备是否参与此类资源重新平衡取决于设备的 [**DEVPKEY \_ device \_ DHP 重新 \_ 平衡 \_ 策略**](../install/devpkey-device-dhp-rebalance-policy.md) 设备属性的设置。 网络适配器中设备 (类 = Net) [设备安装程序类](../install/overview-of-device-setup-classes.md) 的默认行为是，将新处理器动态添加到系统时，它们不会参与资源重新平衡。 所有其他设备安装程序类中的设备的默认行为是在将新处理器动态添加到系统时，它们将参与资源重新平衡。

如果设备是即插即用 (PnP) 设备，并且其参与了这样的资源重新平衡，则在资源重新平衡操作期间，操作系统会将 [**irp \_ MN \_ QUERY \_ 停止 \_ 设备**](./irp-mn-query-stop-device.md)、 [**irp \_ MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md)和 [**irp \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) PnP irp 发送到设备的驱动程序。 这些 PnP 请求通知驱动程序硬件分区中发生硬件更改。 设备驱动程序应通过正确地处理 **IRP \_ MN \_ 查询 \_ 停止 \_ 设备** 和 **IRP \_ MN \_ 停止 \_ 设备** PnP 请求，来支持资源重新平衡。 设备驱动程序绝不应拒绝 **IRP \_ MN \_ 查询 \_ 停止 \_ 设备** PnP 请求。

添加新的处理器后，这些 PnP 请求允许设备驱动程序在硬件分区中充分利用新的活动处理器集。 具体而言，支持资源重新平衡的设备驱动程序使用在资源重新平衡过程中收到的 PnP 请求断开 (Isr 的中断服务例程) 并使用更新的处理器关联值重新连接它们。 这允许设备驱动程序使用硬件分区中所有当前处于活动状态的处理器（包括任何新处理器）来处理中断请求。

设备驱动程序应在重新平衡资源的过程中对所有 i/o 请求进行排队。

有关资源重新平衡的详细信息，请参阅 [停止设备以重新平衡资源](stopping-a-device-to-rebalance-resources.md)。

此方法仅适用于处理器。 将新内存模块添加到硬件分区时，操作系统不会启动系统范围内的资源重新平衡。
