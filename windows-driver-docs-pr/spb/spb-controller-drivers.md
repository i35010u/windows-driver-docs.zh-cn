---
title: SPB 控制器驱动程序
description: 存储控制器是用于控制简单外围总线 （存储） 和传输数据传入和传出连接到存储的外围设备的设备。
ms.assetid: 046353F9-315F-4328-8ECA-1C23AF87B4B4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b701e188158c20605f34a30cdb465b0ce9c8ee0f
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394121"
---
# <a name="spb-controller-drivers"></a>SPB 控制器驱动程序


SPB 控制器是一个设备，该设备控制[简单外设总线](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85)) (SPB) 并可向连接到 SPB 的外围设备传输数据以及从其传输数据。 SPB 控制器的硬件供应商会提供 SPB 控制器驱动程序来管理控制器中的硬件功能。

从 Windows 8 开始，存储框架扩展 (SpbCx) 简化了控制器的驱动程序开发[简单的外围总线](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(SPBs)。 SpbCx 是对系统提供的扩展[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(KMDF)。 存储控制器设备的硬件供应商提供的控制器驱动程序来执行特定于硬件的驱动程序的所有操作。 此驱动程序与 SpbCx 来执行特定于存储控制器的操作进行通信，并直接与 KMDF 执行通用驱动程序操作进行通信。

例如，存储控制器驱动程序通常会调用[ **WdfDeviceInitSetPnpPowerEventCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks) KMDF 注册以接收电源事件的回调，并调用中的方法[ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)方法以从存储控制器连接到中断的驱动程序的中断服务例程 (ISR)。 若要执行特定于存储的操作，与通过 SpbCx 存储控制器通信[SpbCx 设备驱动程序接口](https://docs.microsoft.com/previous-versions/hh698219(v=vs.85))(DDI)。

SpbCx 配合 SBP 控制器驱动程序来处理连接到存储的外围设备的 I/O 请求。 SpbCx 执行通用的存储控制器驱动程序的处理任务。 这些任务包括管理存储控制器的 I/O 请求队列。 这些队列包含来自管理连接到该总线的外围设备的驱动程序的 I/O 请求。 存储控制器驱动程序执行所需处理这些请求的所有特定于硬件的操作。

下图显示了存储控制器驱动程序和 SpbCx。

![存储组件的框图](images/spbmodules.png)

存储控制器驱动程序以及 SpbCx 在内核模式下运行和通过 SpbCx DDI 彼此进行通信。 存储控制器驱动程序调用驱动程序支持的方法，由 SpbCx 实现。 SpbCx 调用事件回叫函数，由存储控制器驱动程序实现。

将 I/O 请求发送到的存储控制器的驱动程序是使用任一内核模式驱动程序[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(KMDF)，或使用的用户模式驱动程序[用户模式驱动程序框架](https://docs.microsoft.com/previous-versions/ff554928(v=vs.85))(UMDF)。 这些驱动程序可以发送读取和写入请求来传输数据传入和传出连接存储的外围设备。 此外，驱动程序可以发送 I/O 控制 (IOCTL) 请求以执行特定于存储的操作。

存储控制器驱动程序直接访问存储控制器设备来启动数据传输到和从连接到存储的外围设备的硬件寄存器。 对于如 I²C 存储，这些数据传输会在相对较慢速度。 尽管可能是内存映射的存储控制器的硬件寄存器，但外围设备的寄存器必须通过存储按顺序访问。

若要将数据传入或从存储连接的外围设备的 I/O 请求的响应，存储控制器驱动程序启动总线传输，将标记为挂起，I/O 请求并返回而无需等待传输完成。 更高版本，存储控制器硬件完成传输，控制器发出信号中断，并在存储控制器驱动程序 ISR 完成挂起的 I/O 请求或启动请求的 I/O 操作中的下一个传输。

驱动程序可以直接向存储控制器发送 I/O 请求。 当在用户模式应用程序将数据传输至存储连接外围设备中，应用程序必须依赖于存储外围设备驱动程序将发送相应的读取或写入请求到的存储控制器。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension" data-raw-source="[SPB Framework Extension (SpbCx)](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)">存储框架扩展 (SpbCx)</a></p></td>
<td><p>从 Windows 8 开始，存储框架扩展 (SpbCx) 是对系统提供的扩展<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers" data-raw-source="[Kernel-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)">内核模式驱动程序框架</a>(KMDF)。 SpbCx 一起使用的工作原理<a href="https://docs.microsoft.com/previous-versions/hh698221(v=vs.85)" data-raw-source="[SPB controller driver](https://docs.microsoft.com/previous-versions/hh698221(v=vs.85))">存储控制器驱动程序</a>若要执行的已连接到外围设备上的 I/O 操作<a href="https://docs.microsoft.com/previous-versions/hh450903(v=vs.85)" data-raw-source="[simple peripheral bus](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))">简单的外围总线</a>（存储），如 I²C 或 SPI。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spbcx-interfaces" data-raw-source="[SpbCx Interfaces](https://docs.microsoft.com/windows-hardware/drivers/spb/spbcx-interfaces)">SpbCx 接口</a></p></td>
<td><p>存储框架扩展 (SpbCx) 有两个接口。 首先，通过该 SpbCx 接受 I/O 请求的存储控制器的客户端 （外围设备驱动程序） 发送到连接到总线的外围设备的 I/O 请求接口。 第二个接口是通过其 SpbCx 与存储控制器驱动程序进行通信的设备驱动程序接口 (DDI)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences" data-raw-source="[I/O Transfer Sequences](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)">I/O 传输序列</a></p></td>
<td><p>存储框架扩展 (SpbCx) 支持 I/O 传输序列。 I/O 传输序列是一组有序的总线传输 （读取和写入操作），作为单个、 原子总线操作执行。 在 I/O 传输序列中传输的所有访问总线上相同的目标设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/handling-client-implemented-sequences" data-raw-source="[Handling Client-Implemented Sequences](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-client-implemented-sequences)">处理客户端实现序列</a></p></td>
<td><p>可选<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_controller_lock" data-raw-source="[&lt;em&gt;EvtSpbControllerLock&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_controller_lock)"> <em>EvtSpbControllerLock</em> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_controller_unlock" data-raw-source="[&lt;em&gt;EvtSpbControllerUnlock&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_controller_unlock)"> <em>EvtSpbControllerUnlock</em> </a>事件回调函数执行的补充操作。 <em>EvtSpbControllerLock</em>函数是一个处理程序<a href="https://msdn.microsoft.com/library/windows/hardware/hh450858" data-raw-source="[&lt;strong&gt;IOCTL_SPB_LOCK_CONTROLLER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450858)"> <strong>IOCTL_SPB_LOCK_CONTROLLER</strong> </a>请求。 <em>EvtSpbControllerUnlock</em>函数是一个处理程序<a href="https://msdn.microsoft.com/library/windows/hardware/hh450859" data-raw-source="[&lt;strong&gt;IOCTL_SPB_UNLOCK_CONTROLLER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh450859)"> <strong>IOCTL_SPB_UNLOCK_CONTROLLER</strong> </a>请求。 客户端 （即，总线上外围设备的驱动程序） 将发送这些请求开始和结束<a href="https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences" data-raw-source="[I/O transfer sequences](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)">I/O 传输序列</a>。 大多数存储控制器驱动程序不支持<strong>IOCTL_SPB_LOCK_CONTROLLER</strong>并<strong>IOCTL_SPB_UNLOCK_CONTROLLER</strong>请求并且因此，不实现<em>EvtSpbControllerLock</em>并<em>EvtSpbControllerUnlock</em>函数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/using-the-spb-transfer-list-structure" data-raw-source="[Using the SPB_TRANSFER_LIST Structure for Custom IOCTLs](https://docs.microsoft.com/windows-hardware/drivers/spb/using-the-spb-transfer-list-structure)">使用自定义 Ioctl SPB_TRANSFER_LIST 结构</a></p></td>
<td><p>如果您的简单外围总线 （存储） 控制器驱动程序支持一个或多个自定义的 I/O 控制 (IOCTL) 请求，使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spb/ns-spb-spb_transfer_list" data-raw-source="[&lt;strong&gt;SPB_TRANSFER_LIST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spb/ns-spb-spb_transfer_list)"> <strong>SPB_TRANSFER_LIST</strong> </a>结构描述读取和写入缓冲区中这些请求数。 此结构提供了统一的方式来描述在请求中，缓冲区，可以避免 METHOD_BUFFERED I/O 操作相关联的缓冲区复制开销。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests" data-raw-source="[Handling IOCTL_SPB_FULL_DUPLEX Requests](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests)">处理 IOCTL_SPB_FULL_DUPLEX 请求</a></p></td>
<td><p>某些总线，SPI，例如启用读取和写入传输总线控制器和总线上的设备之间同时发生。 若要支持这些全双工传输，简单的外围总线 （存储） I/O 请求接口的定义包括，作为一个选项， <a href="https://msdn.microsoft.com/library/windows/hardware/hh974774" data-raw-source="[&lt;strong&gt;IOCTL_SPB_FULL_DUPLEX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh974774)"> <strong>IOCTL_SPB_FULL_DUPLEX</strong> </a> I/O 控制代码 (IOCTL)。 仅存储控制器驱动程序的硬件中实现全双工传输总线控制器应支持<strong>IOCTL_SPB_FULL_DUPLEX</strong> IOCTL。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/spb/how-to-get-the-connection-settings-for-a-device" data-raw-source="[How to Get the Connection Settings for a Device](https://docs.microsoft.com/windows-hardware/drivers/spb/how-to-get-the-connection-settings-for-a-device)">如何获取设备的连接设置</a></p></td>
<td><p>如果您的存储控制器驱动程序注册<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_target_connect" data-raw-source="[&lt;em&gt;EvtSpbTargetConnect&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_target_connect)"> <em>EvtSpbTargetConnect</em> </a>回调函数<a href="https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension" data-raw-source="[SPB framework extension](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)">存储框架扩展</a>(SpbCx) 调用此函数时客户端 （外围设备驱动程序） 的控制器发送<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)"> <strong>IRP_MJ_CREATE</strong> </a>请求以打开到总线上的目标设备的逻辑连接。 以响应<em>EvtSpbTargetConnect</em>回调，存储控制器驱动程序应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbtargetgetconnectionparameters" data-raw-source="[&lt;strong&gt;SpbTargetGetConnectionParameters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbtargetgetconnectionparameters)"> <strong>SpbTargetGetConnectionParameters</strong> </a>方法以获取连接目标设备的设置。 存储控制器驱动程序将这些设置存储和更高版本使用它们来访问响应来自客户端的 I/O 请求中的设备。</p></td>
</tr>
</tbody>
</table>

 

 

 




