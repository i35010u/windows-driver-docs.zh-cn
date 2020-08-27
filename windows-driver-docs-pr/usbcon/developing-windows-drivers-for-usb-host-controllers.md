---
description: 为 USB 主控制器开发 Windows 驱动程序
title: 为 USB 主控制器开发 Windows 驱动程序的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e79571b22d52878423b389473df0cceb7315547
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968990"
---
# <a name="overview-of-developing-windows-drivers-for-usb-host-controllers"></a>为 USB 主控制器开发 Windows 驱动程序的概述


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>目的</strong></p>
<p>本部分介绍 Windows 操作系统中的支持，用于开发与 Microsoft 提供的 USB 主机控制器扩展 (UCX) 通信的通用串行总线 (USB) 主机控制器驱动程序。</p>
<p>如果开发不符合规格的 xHCI 主控制器，或者开发自定义的非 xHCI 硬件（例如虚拟主控制器），则可编写可以与 UCX 通信的主控制器驱动程序。 例如，可以考虑支持 USB 设备的无线坞。 电脑通过无线坞与 USB 设备通信，使用基于 TCP 的 USB 作为传输方式。</p>
<p><strong>USB 主控制器扩展 (UCX)</strong></p>
<p>USB 主机控制器扩展是系统提供的驱动程序 ( # A0) 。 此驱动程序通过使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/" data-raw-source="[Windows Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/)">Windows 驱动程序框架</a> 编程接口实现为框架类扩展。 主机控制器驱动程序充当该类扩展的客户端驱动程序。 当主机控制器驱动程序处理硬件操作和事件、电源管理和 PnP 事件时，UCX 充当抽象接口，该接口将请求发送到主机控制器驱动程序，并执行其他任务。</p>
<p>UCX 是 <a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows 中的一个 USB 主机端驱动程序</a>。 它作为主机控制器设备堆栈中的 FDO 加载。</p>
<p><strong>USB 主机控制器驱动程序</strong></p>
<p>UCX 是可扩展的，旨在支持各种主机控制器驱动程序。 Windows 提供了 xHCI 驱动程序 ( # A0) 以 USB xHCI 主机控制器为目标。</p>
<p>主机控制器驱动程序是 UCX 的客户端，作为 <a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging" data-raw-source="[Kernel-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging)">内核模式驱动程序框架</a> 写入 (KMDF) 驱动程序。</p>
<p><strong>Microsoft 提供的二进制文件</strong></p>
<p>若要编写主机控制器驱动程序，需要 UCX ( # A0) 和存根库 (Ucx01000) 。 存根库位于 Windows 驱动程序工具包中 (WDK) 。 库执行两个主要功能。</p>
<ul>
<li>转换主机控制器驱动程序发出的调用，并将其传递给 UCX。</li>
<li>为版本控制提供支持。 仅当 UCX 与主机控制器驱动程序的主版本号相同，并且主机控制器驱动程序的版本号相同或更高时，主机控制器驱动程序才能使用 UCX。</li>
</ul>
<p><strong>开发工具</strong></p>
<p>WDK 包含驱动程序开发所需的资源，如标头、库、工具和示例。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">下载适用于 Windows 的工具包和工具</a></p></td>
<td><p><strong>入门 .。。</strong></p>
<p>阅读用于描述体系结构 (设备、主机控制器和中心) 的不同组件的预期行为的官方规范。</p>
<a href="https://go.microsoft.com/fwlink/p/?linkid=618273" data-raw-source="[xHCI for Universal Serial Bus: Specification]( https://go.microsoft.com/fwlink/p/?linkid=618273)">适用于通用串行总线的 xHCI：规范</a>
<a href="https://go.microsoft.com/fwlink/p/?linkid=224892" data-raw-source="[Official Universal Serial Bus Documents]( https://go.microsoft.com/fwlink/p/?linkid=224892)">官方通用串行总线文档</a>
<p><strong>了解 UCX 的体系结构</strong></p>
<p>熟悉 Microsoft 提供的 USB 驱动程序堆栈：</p>
<a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows 中的 usb 主机端驱动程序</a>
<a href="get-started-with-host-controller-driver-development.md" data-raw-source="[Architecture: USB host controller extension (UCX)](get-started-with-host-controller-driver-development.md)">体系结构： usb 主机控制器扩展 (UCX) </a>
<p><strong>熟悉 UCX 对象和句柄</strong></p>
<p>UCX 扩展了 WDF 对象功能，以定义其自己的特定于 USB 的 UCX 对象。 有关 WDF 对象的更多详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects" data-raw-source="[Introduction to Framework Objects](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)">框架对象简介</a>。</p>
<p>对于对任何底层主机控制器驱动程序的请求排队，UCX 将使用这些对象。 有关详细信息，请参阅 <a href="ucx-objects-and-handles-used-by-host-controller-driver.md" data-raw-source="[UCX objects and handles used by a host controller driver](ucx-objects-and-handles-used-by-host-controller-driver.md)">UCX 对象和主机控制器驱动程序使用的句柄</a>。</p>
<p></p>
<dl>
<dt>主机控制器对象 (UCXCONTROLLER) </dt>
<dd><p>表示主机控制器驱动程序创建的主控制器。 驱动程序必须为每个主机控制器实例仅创建一个主机控制器对象。 通常通过调用<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85)" data-raw-source="[&lt;strong&gt;UcxControllerCreate&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))"><strong>UcxControllerCreate</strong></a>方法在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add" data-raw-source="[**EVT_WDF_DRIVER_DEVICE_ADD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)"><strong>EVT_WDF_DRIVER_DEVICE_ADD</strong></a>回调中创建。</p>
</dd>
<dt>根中心对象 (UCXROOTHUB) </dt>
<dd><p>获取和控制主机控制器的根端口的状态。 通常通过调用<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188048(v=vs.85)" data-raw-source="[&lt;strong&gt;UcxRootHubCreate&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188048(v=vs.85))"><strong>UcxRootHubCreate</strong></a>方法，由主机控制器驱动程序在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add" data-raw-source="[**EVT_WDF_DRIVER_DEVICE_ADD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)"><strong>EVT_WDF_DRIVER_DEVICE_ADD</strong></a>回调中创建。</p>
</dd>
<dt>USB 设备对象 (UCXUSBDEVICE) </dt>
<dd><p>表示连接到总线的物理 USB 设备。 通常通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate" data-raw-source="[&lt;strong&gt;UcxUsbDeviceCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate)"><strong>UcxUsbDeviceCreate</strong></a>方法，由主机控制器驱动程序在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_usbdevice_add" data-raw-source="[&lt;em&gt;EVT_UCX_CONTROLLER_USBDEVICE_ADD&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_usbdevice_add)"><em>EVT_UCX_CONTROLLER_USBDEVICE_ADD</em></a>回调中创建。</p>
</dd>
<dt>终结点对象 (UCXENDPOINT) </dt>
<dd><p>表示 USB 设备对象上的终结点。 由主机控制器驱动程序通常在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_default_endpoint_add" data-raw-source="[&lt;em&gt;EVT_UCX_USBDEVICE_DEFAULT_ENDPOINT_ADD&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_default_endpoint_add)"><em>EVT_UCX_USBDEVICE_DEFAULT_ENDPOINT_ADD</em></a>内创建，或通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointcreate" data-raw-source="[&lt;strong&gt;UcxEndpointCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointcreate)"><strong>UcxEndpointCreate</strong></a>方法<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoint_add" data-raw-source="[&lt;em&gt;EVT_UCX_USBDEVICE_ENDPOINT_ADD&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoint_add)"><em>EVT_UCX_USBDEVICE_ENDPOINT_ADD</em></a>回调。</p>
</dd>
<dt>Stream 对象 (UCXSTREAMS) </dt>
<dd><p>跨单个大容量终结点表示设备的多个管道。 通常通过调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamscreate" data-raw-source="[&lt;strong&gt;UcxStaticStreamsCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamscreate)"><strong>UcxStaticStreamsCreate</strong></a>方法，由主机控制器驱动程序在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_add" data-raw-source="[&lt;em&gt;EVT_UCX_ENDPOINT_STATIC_STREAMS_ADD&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_add)"><em>EVT_UCX_ENDPOINT_STATIC_STREAMS_ADD</em></a>回调中创建。</p>
</dd>
</dl>
<p><strong>文档部分</strong></p>
<a href="manage-the-root-hub-in-a-host-controller-driver.md" data-raw-source="[Root hub callback functions of a host controller driver](manage-the-root-hub-in-a-host-controller-driver.md)">主机控制器驱动程序的根中心回调函数</a>
<p>UCX 处理与根集线器相关的大多数操作。 这允许 USB 集线器驱动程序与根集线器交互，其方式与与常规中心交互的方式相同。 主机控制器驱动程序可以注册它的回调函数。</p>
<a href="handling-i-o-requests-in-a-host-controller-driver.md" data-raw-source="[Handle I/O requests in a USB host controller driver](handling-i-o-requests-in-a-host-controller-driver.md)">处理 USB 主机控制器驱动程序中的 i/o 请求</a>
<p>UCX 会审传入 USB 请求块 (URBs) ，然后将其转发到正确的终结点队列。</p>
<a href="configuring-usb-endpoints-in-a-host-controller-driver.md" data-raw-source="[Configure USB endpoints in a host controller driver](configuring-usb-endpoints-in-a-host-controller-driver.md)">在主机控制器驱动程序中配置 USB 端点</a>
<p>主机控制器驱动程序在 UCX 管理与终结点关联的队列以及将终结点编程到控制器硬件中扮演着一个角色。</p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#host-controller-driver-reference" data-raw-source="[USB host controller extension (UCX) reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#host-controller-driver-reference)">USB 主机控制器扩展 (UCX) 参考</a>
<p>提供客户端驱动程序使用的 i/o 请求、支持例程、结构和接口的规范。 这些例程和相关的数据结构在 WDK 头文件中定义。</p>
<p>UCX 称为 <em>框架类扩展</em>。</p>
<p>主机控制器驱动程序称为 " <em>客户端驱动程序</em>"。</p></td>

</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



