---
Description: Developing Windows drivers for USB host controllers
title: 为 USB 主控制器开发 Windows 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cee2cfac0dd75e730bf43ce1307ea73279dcaf3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568422"
---
# <a name="developing-windows-drivers-for-usb-host-controllers"></a>为 USB 主控制器开发 Windows 驱动程序


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>用途</strong></p>
<p>本部分介绍用于开发与 Microsoft 提供的 USB 主机控制器扩展 (UCX) 进行通信的通用串行总线 (USB) 主机控制器驱动程序的 Windows 操作系统系统中的支持。</p>
<p>如果开发不符合规格的 xHCI 主控制器，或者开发自定义的非 xHCI 硬件（例如虚拟主控制器），则可编写可以与 UCX 通信的主控制器驱动程序。 例如，可以考虑支持 USB 设备的无线坞。 电脑通过无线坞与 USB 设备通信，使用基于 TCP 的 USB 作为传输方式。</p>
<p><strong>USB 主机控制器扩展 (UCX)</strong></p>
<p>USB 主机控制器扩展是系统提供的驱动程序 (Ucx01000.sys)。 此驱动程序使用为框架类扩展实施<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/" data-raw-source="[Windows Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/)">Windows 驱动程序框架</a>编程接口。 主机控制器驱动程序可用作对该类扩展的客户端驱动程序。 而主机控制器驱动程序来处理硬件操作和事件、 电源管理和即插即用事件，UCX 用作主机控制器驱动程序，对请求进行排队并执行其他任务的抽象接口。</p>
<p>UCX 是之一<a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">USB 宿主端驱动程序在 Windows 中的</a>。 作为主机控制器设备堆栈中 FDO 加载它。</p>
<p><strong>USB 主控制器驱动程序</strong></p>
<p>UCX 是可扩展的旨在支持各种主机控制器驱动程序。 Windows 提供 xHCI 驱动程序 (Usbxhci.sys) 该目标 USB xHCI 主控制器。</p>
<p>主机控制器驱动程序是一个客户端的 UCX，写作<a href="https://msdn.microsoft.com/library/windows/hardware/ff551869" data-raw-source="[Kernel-Mode Driver Framework](https://msdn.microsoft.com/library/windows/hardware/ff551869)">内核模式驱动程序框架</a>(KMDF) 驱动程序。</p>
<p><strong>Microsoft 提供的二进制文件</strong></p>
<p>若要编写宿主控制器驱动程序，需要 UCX (Ucx01000.sys) 和存根 （stub） 库 (Ucx01000.lib)。 存根 （stub） 库是 Windows Driver Kit (WDK) 中。 库执行两个主要功能。</p>
<ul>
<li>将所做的主机控制器驱动程序的调用转换为并将其传递到 UCX。</li>
<li>提供对版本控制支持。 主机控制器驱动程序将使用 UCX，仅当 UCX 具有相同的主要版本号作为主机控制器驱动程序，并且相同或更高版本的次要版本号作为主机控制器驱动程序。</li>
</ul>
<p><strong>开发工具</strong></p>
<p>WDK 包含所需的驱动程序开发，例如标头、 库、 工具和示例的资源。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">下载适用于 Windows 的工具包和工具</a></p></td>
<td><p><strong>获取已启动...</strong></p>
<p>阅读官方规范描述体系结构的不同组件 （设备、 主控制器和中心） 的预期的行为。</p>
<a href="https://go.microsoft.com/fwlink/p/?linkid=618273" data-raw-source="[xHCI for Universal Serial Bus: Specification]( https://go.microsoft.com/fwlink/p/?linkid=618273)">为通用串行总线 xHCI:规范</a>
<a href="https://go.microsoft.com/fwlink/p/?linkid=224892" data-raw-source="[Official Universal Serial Bus Documents]( https://go.microsoft.com/fwlink/p/?linkid=224892)">官方通用串行总线文档</a>
<p><strong>了解 UCX 的体系结构</strong></p>
<p>熟悉 Microsoft 提供的 USB 驱动程序堆栈：</p>
<a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">在 Windows 中的 USB 宿主端驱动程序</a>
<a href="get-started-with-host-controller-driver-development.md" data-raw-source="[Architecture: USB host controller extension (UCX)](get-started-with-host-controller-driver-development.md)">体系结构：USB 主机控制器扩展 (UCX)</a>
<p><strong>熟悉 UCX 对象和句柄</strong></p>
<p>UCX 扩展了 WDF 对象功能来定义其自己特定于 USB 的 UCX 对象。 WDF 对象的更多详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff544249" data-raw-source="[Introduction to Framework Objects](https://msdn.microsoft.com/library/windows/hardware/ff544249)">Framework 对象简介</a>。</p>
<p>对于任何基础主机控制器驱动程序的队列请求，UCX 使用这些对象。 有关详细信息，请参阅<a href="ucx-objects-and-handles-used-by-host-controller-driver.md" data-raw-source="[UCX objects and handles used by a host controller driver](ucx-objects-and-handles-used-by-host-controller-driver.md)">UCX 对象和处理主机控制器驱动程序使用的</a>。</p>
<p></p>
<dl>
<dt>主机控制器对象 (UCXCONTROLLER)</dt>
<dd><p>表示创建的主机控制器驱动程序的主机控制器。 该驱动程序必须创建每个主机控制器实例只有一个主机控制器对象。 通常在中创建<a href="https://msdn.microsoft.com/library/windows/hardware/ff541693" data-raw-source="[**EVT_WDF_DRIVER_DEVICE_ADD**](https://msdn.microsoft.com/library/windows/hardware/ff541693)"> <strong>EVT_WDF_DRIVER_DEVICE_ADD</strong></a>通过调用回调<a href="https://msdn.microsoft.com/library/windows/hardware/mt188033" data-raw-source="[&lt;strong&gt;UcxControllerCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt188033)"> <strong>UcxControllerCreate</strong> </a>方法。</p>
</dd>
<dt>根中心对象 (UCXROOTHUB)</dt>
<dd><p>获取并控制主控制器的根端口的状态。 通常在创建的主机控制器驱动程序<a href="https://msdn.microsoft.com/library/windows/hardware/ff541693" data-raw-source="[**EVT_WDF_DRIVER_DEVICE_ADD**](https://msdn.microsoft.com/library/windows/hardware/ff541693)"> <strong>EVT_WDF_DRIVER_DEVICE_ADD</strong> </a>通过调用回调<a href="https://msdn.microsoft.com/library/windows/hardware/mt188048" data-raw-source="[&lt;strong&gt;UcxRootHubCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt188048)"> <strong>UcxRootHubCreate</strong> </a>方法。</p>
</dd>
<dt>USB 设备对象 (UCXUSBDEVICE)</dt>
<dd><p>表示物理 USB 设备连接到总线。 通常在创建的主机控制器驱动程序<a href="https://msdn.microsoft.com/library/windows/hardware/mt187823" data-raw-source="[&lt;em&gt;EVT_UCX_CONTROLLER_USBDEVICE_ADD&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/mt187823)"> <em>EVT_UCX_CONTROLLER_USBDEVICE_ADD</em> </a>通过调用回调<a href="https://msdn.microsoft.com/library/windows/hardware/mt188052" data-raw-source="[&lt;strong&gt;UcxUsbDeviceCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt188052)"> <strong>UcxUsbDeviceCreate</strong></a>方法。</p>
</dd>
<dt>终结点对象 (UCXENDPOINT)</dt>
<dd><p>表示一个 USB 设备对象上的终结点。 通常在创建的主机控制器驱动程序<a href="https://msdn.microsoft.com/library/windows/hardware/mt187839" data-raw-source="[&lt;em&gt;EVT_UCX_USBDEVICE_DEFAULT_ENDPOINT_ADD&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/mt187839)"> <em>EVT_UCX_USBDEVICE_DEFAULT_ENDPOINT_ADD</em> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/mt187843" data-raw-source="[&lt;em&gt;EVT_UCX_USBDEVICE_ENDPOINT_ADD&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/mt187843)"> <em>EVT_UCX_USBDEVICE_ENDPOINT_ADD</em></a>通过调用回调<a href="https://msdn.microsoft.com/library/windows/hardware/mt188039" data-raw-source="[&lt;strong&gt;UcxEndpointCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt188039)"> <strong>UcxEndpointCreate</strong> </a>方法。</p>
</dd>
<dt>Stream 对象 (UCXSTREAMS)</dt>
<dd><p>表示单个批量终结点设备的管道数。 通常在创建的主机控制器驱动程序<a href="https://msdn.microsoft.com/library/windows/hardware/mt187830" data-raw-source="[&lt;em&gt;EVT_UCX_ENDPOINT_STATIC_STREAMS_ADD&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/mt187830)"> <em>EVT_UCX_ENDPOINT_STATIC_STREAMS_ADD</em> </a>通过调用回调<a href="https://msdn.microsoft.com/library/windows/hardware/mt188050" data-raw-source="[&lt;strong&gt;UcxStaticStreamsCreate&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt188050)"> <strong>UcxStaticStreamsCreate</strong></a>方法。</p>
</dd>
</dl>
<p><strong>文档部分</strong></p>
<a href="manage-the-root-hub-in-a-host-controller-driver.md" data-raw-source="[Root hub callback functions of a host controller driver](manage-the-root-hub-in-a-host-controller-driver.md)">主机控制器驱动程序的根中心回调函数</a>
<p>UCX 处理与根 hub 相关的大多数操作。 这允许 USB 集线器驱动程序，以便它与常规中心进行交互一样与根集线器。 主机控制器驱动程序可以注册其回调函数。</p>
<a href="handling-i-o-requests-in-a-host-controller-driver.md" data-raw-source="[Handle I/O requests in a USB host controller driver](handling-i-o-requests-in-a-host-controller-driver.md)">USB 主控制器驱动程序中处理 I/O 请求</a>
<p>UCX 会审传入 USB 请求阻止 (URBs)，然后将其转发到正确的终结点队列。</p>
<a href="configuring-usb-endpoints-in-a-host-controller-driver.md" data-raw-source="[Configure USB endpoints in a host controller driver](configuring-usb-endpoints-in-a-host-controller-driver.md)">主机控制器驱动程序中配置 USB 终结点</a>
<p>主机控制器驱动程序在其终结点，与关联的队列的 UCX 的管理，控制器硬件到终结点的编程中发挥着作用。</p>
<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#host-controller-driver-reference" data-raw-source="[USB host controller extension (UCX) reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#host-controller-driver-reference)">USB 主机控制器扩展 (UCX) 参考</a>
<p>提供用于 I/O 请求、 支持例程、 结构和使用的客户端驱动程序接口规范。 WDK 标头中定义这些例程和相关的数据结构。</p>
<p>UCX 称为<em>框架类扩展</em>。</p>
<p>主机控制器驱动程序被称为<em>客户端驱动程序</em>。</p></td>

</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  



