---
title: SPB 控制器驱动程序
description: SPB 控制器是一个设备，该设备控制简单外设总线 (SPB) 并可向连接到 SPB 的外围设备传输数据以及从其传输数据。
ms.assetid: 046353F9-315F-4328-8ECA-1C23AF87B4B4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c0b24d6a79232ef5644cfd026cefe4f0e33f3b7
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106190"
---
# <a name="spb-controller-drivers"></a>SPB 控制器驱动程序


SPB 控制器是一个设备，该设备控制[简单外设总线](/previous-versions/hh450903(v=vs.85)) (SPB) 并可向连接到 SPB 的外围设备传输数据以及从其传输数据。 SPB 控制器的硬件供应商会提供 SPB 控制器驱动程序来管理控制器中的硬件功能。

从 Windows 8 开始，SPB framework 扩展 (SpbCx) 简化了 (SPBs) 的 [简单外围总线](/previous-versions/hh450903(v=vs.85)) 的控制器驱动程序的开发。 SpbCx 是系统提供的针对 [内核模式驱动程序框架](../wdf/index.md) 的扩展 (KMDF) 。 SPB 控制器设备的硬件供应商提供控制器驱动程序来执行所有硬件特定的驱动程序操作。 此驱动程序与 SpbCx 通信以执行特定于 SPB 控制器的操作，并直接与 KMDF 进行通信以执行一般的驱动程序操作。

例如，SPB 控制器驱动程序通常会调用 KMDF 中的 [**WdfDeviceInitSetPnpPowerEventCallbacks**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks) 方法来注册来接收电源事件回调，并调用 [**WdfInterruptCreate**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) 方法将驱动程序的中断服务例程连接 (ISR) 从 SPB 控制器中断。 为了执行特定于 SPB 的操作，SPB 控制器通过 [SpbCx 设备驱动程序接口](/previous-versions/hh698219(v=vs.85)) 与 SpbCx 通信， (DDI) 。

SpbCx 会和 SBP 控制器驱动程序，用于处理连接到 SPB 的外围设备的 i/o 请求。 SpbCx 执行由 SPB 控制器驱动程序公用的处理任务。 这些任务包括管理 SPB 控制器的 i/o 请求队列。 这些队列包含来自管理连接到总线的外围设备的驱动程序的 i/o 请求。 SPB 控制器驱动程序执行处理这些请求所需的所有特定于硬件的操作。

下图显示了 SPB 控制器驱动程序和 SpbCx。

![spb 组件框图](images/spbmodules.png)

SPB 控制器驱动程序和 SpbCx 都在内核模式下运行，并通过 SpbCx DDI 相互通信。 SPB 控制器驱动程序调用由 SpbCx 实现的驱动程序支持方法。 SpbCx 调用由 SPB 控制器驱动程序实现的事件回调函数。

将 i/o 请求发送到 SPB 控制器的驱动程序为使用 [内核模式驱动程序框架](../wdf/index.md) (KMDF) 的内核模式驱动程序，或使用 [用户模式驱动程序框架](/previous-versions/ff554928(v=vs.85)) (UMDF) 的用户模式驱动程序。 这些驱动程序可以发送读写请求，以便将数据传入和传出由 SPB 连接的外围设备。 此外，驱动程序可以将 i/o 控制 (IOCTL 发送) 请求来执行 SPB 特定的操作。

SPB 控制器驱动程序直接访问 SPB 控制器设备的硬件寄存器，以启动与连接到 SPB 的外围设备之间的数据传输。 对于诸如 i2c 这样的 SPB，这些数据传输的速度相对较慢。 尽管 SPB 控制器的硬件寄存器可能是内存映射的，但必须通过 SPB 串行访问外围设备的寄存器。

为了响应将数据传入或传出连接到 SPB 的外围设备的 i/o 请求，SPB 控制器驱动程序将启动总线传输，将 i/o 请求标记为挂起，并返回而不等待传输完成。 稍后，当 SPB 控制器硬件完成了传输时，控制器会向中断发出信号，而 SPB 控制器驱动程序中的 ISR 将完成挂起的 i/o 请求，或在请求的 i/o 操作中启动下一次传输。

只有驱动程序可以将 i/o 请求直接发送到 SPB 控制器。 当用户模式应用程序在连接到 SPB 的外设之间传输数据时，应用程序必须依赖于 SPB 外围设备驱动程序，以将相应的读取或写入请求发送到 SPB 控制器。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/spb/spb-framework-extension" data-raw-source="[SPB Framework Extension (SpbCx)](./spb-framework-extension.md)">SPB 框架扩展 (SpbCx)</a></p></td>
<td><p>从 Windows 8 开始，SPB 框架扩展 (SpbCx) 是系统提供的针对 <a href="/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers" data-raw-source="[Kernel-Mode Driver Framework](../wdf/index.md)">内核模式驱动程序框架</a> 的扩展 (KMDF) 。 SpbCx 与 <a href="/previous-versions/hh698221(v=vs.85)" data-raw-source="[SPB controller driver](/previous-versions/hh698221(v=vs.85))">SPB 控制器驱动程序</a> 一起工作，以对连接到 <a href="/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](/previous-versions/hh450903(v=vs.85))">简单外围总线</a> (SPB) （如 I i2c 或 SPI）的外围设备执行 i/o 操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/spb/spbcx-interfaces" data-raw-source="[SpbCx Interfaces](./spbcx-interfaces.md)">SpbCx 接口</a></p></td>
<td><p>SPB 框架扩展 (SpbCx) 有两个接口。 第一种是 i/o 请求接口，通过该接口，SpbCx 可接受 i/o 请求，客户端 (外围设备驱动程序) 的 SPB 控制器发送到连接到总线的外围设备。 第二个接口是设备驱动程序接口 (DDI) ，SpbCx 与 SPB 控制器驱动程序通信。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/spb/i-o-transfer-sequences" data-raw-source="[I/O Transfer Sequences](./i-o-transfer-sequences.md)">I/O 传输序列</a></p></td>
<td><p>SPB 框架扩展 (SpbCx) 支持 i/o 传输顺序。 I/o 传输序列是一组有序的总线传输 (读取和写入操作，作为单个原子总线操作执行) 。 I/o 传输序列中的所有传输在总线上访问相同的目标设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/spb/handling-client-implemented-sequences" data-raw-source="[Handling Client-Implemented Sequences](./handling-client-implemented-sequences.md)">处理客户端实现的序列</a></p></td>
<td><p>可选的 <a href="/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_lock" data-raw-source="[&lt;em&gt;EvtSpbControllerLock&lt;/em&gt;](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_lock)"><em>EvtSpbControllerLock</em></a> 和 <a href="/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_unlock" data-raw-source="[&lt;em&gt;EvtSpbControllerUnlock&lt;/em&gt;](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_unlock)"><em>EvtSpbControllerUnlock</em></a> 事件回调函数执行互补运算。 <em>EvtSpbControllerLock</em>函数是用于<a href="https://msdn.microsoft.com/library/windows/hardware/hh450858" data-raw-source="[&lt;strong&gt;IOCTL_SPB_LOCK_CONTROLLER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450858)"><strong>IOCTL_SPB_LOCK_CONTROLLER</strong></a>请求的处理程序。 <em>EvtSpbControllerUnlock</em>函数是用于<a href="https://msdn.microsoft.com/library/windows/hardware/hh450859" data-raw-source="[&lt;strong&gt;IOCTL_SPB_UNLOCK_CONTROLLER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450859)"><strong>IOCTL_SPB_UNLOCK_CONTROLLER</strong></a>请求的处理程序。 客户端 (即，总线上的外围设备的驱动程序) 将这些请求发送到开始和结束 <a href="/windows-hardware/drivers/spb/i-o-transfer-sequences" data-raw-source="[I/O transfer sequences](./i-o-transfer-sequences.md)">i/o 传输序列</a>。 大多数 SPB 控制器驱动程序不支持 <strong>IOCTL_SPB_LOCK_CONTROLLER</strong> 和 <strong>IOCTL_SPB_UNLOCK_CONTROLLER</strong> 请求，因此不实现 <em>EvtSpbControllerLock</em> 和 <em>EvtSpbControllerUnlock</em> 函数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/spb/using-the-spb-transfer-list-structure" data-raw-source="[Using the SPB_TRANSFER_LIST Structure for Custom IOCTLs](./using-the-spb-transfer-list-structure.md)">将 SPB_TRANSFER_LIST 结构用于自定义 IOCTL</a></p></td>
<td><p>如果你的简单外围总线 (SPB) 控制器驱动程序支持一个或多个自定义 i/o 控件 (IOCTL) 请求，请使用 <a href="/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list" data-raw-source="[&lt;strong&gt;SPB_TRANSFER_LIST&lt;/strong&gt;](/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list)"><strong>SPB_TRANSFER_LIST</strong></a> 结构来描述这些请求中的读取和写入缓冲区。 此结构提供了一种统一的方法来描述请求中的缓冲区，并避免与 METHOD_BUFFERED i/o 操作相关的缓冲区复制开销。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests" data-raw-source="[Handling IOCTL_SPB_FULL_DUPLEX Requests](./handling-ioctl-spb-full-duplex-requests.md)">处理 IOCTL_SPB_FULL_DUPLEX 请求</a></p></td>
<td><p>某些总线，如 SPI，可在总线控制器和总线上的设备之间同时进行读取和写入传输。 为了支持这些全双工传输，简单外围总线 (SPB) i/o 请求接口的定义包括 <a href="https://msdn.microsoft.com/library/windows/hardware/hh974774" data-raw-source="[&lt;strong&gt;IOCTL_SPB_FULL_DUPLEX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh974774)"><strong>IOCTL_SPB_FULL_DUPLEX</strong></a> i/o 控制代码 (IOCTL) 的选项。 仅在硬件中实现全双工传输的总线控制器的 SPB 控制器驱动程序应支持 <strong>IOCTL_SPB_FULL_DUPLEX</strong> 的 IOCTL。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/spb/how-to-get-the-connection-settings-for-a-device" data-raw-source="[How to Get the Connection Settings for a Device](./how-to-get-the-connection-settings-for-a-device.md)">如何获取设备的连接设置</a></p></td>
<td><p>如果你的 SPB 控制器驱动程序注册了一个<a href="/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_connect" data-raw-source="[&lt;em&gt;EvtSpbTargetConnect&lt;/em&gt;](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_connect)"><em>EvtSpbTargetConnect</em></a>回调函数，则当控制器的客户端 (外设驱动程序) 发送<a href="/windows-hardware/drivers/kernel/irp-mj-create" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](../kernel/irp-mj-create.md)"><strong>IRP_MJ_CREATE</strong></a>请求以打开与总线上的目标设备的逻辑连接时， <a href="/windows-hardware/drivers/spb/spb-framework-extension" data-raw-source="[SPB framework extension](./spb-framework-extension.md)">spb framework 扩展</a> (SpbCx) 调用此函数。 为了响应 <em>EvtSpbTargetConnect</em> 回调，SPB 控制器驱动程序应调用 <a href="/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetconnectionparameters" data-raw-source="[&lt;strong&gt;SpbTargetGetConnectionParameters&lt;/strong&gt;](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetconnectionparameters)"><strong>SpbTargetGetConnectionParameters</strong></a> 方法来获取目标设备的连接设置。 SPB 控制器驱动程序将存储这些设置，并在以后使用它们来访问设备，以响应客户端发出的 i/o 请求。</p></td>
</tr>
</tbody>
</table>

 

