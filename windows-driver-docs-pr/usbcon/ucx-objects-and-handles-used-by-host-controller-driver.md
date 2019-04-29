---
Description: UCX 扩展了 WDF 对象功能来定义其自己特定于 USB 的 UCX 对象。 UCX 队列请求任何基础主机控制器驱动程序使用这些对象。
title: 主控制器驱动程序使用的 UCX 对象和句柄
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43989c34cb5e345b3c082f8e9215a94bc3cf85e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355178"
---
# <a name="ucx-objects-and-handles-used-by-a-host-controller-driver"></a>主控制器驱动程序使用的 UCX 对象和句柄


**摘要**

-   UCX 对象由主机控制器驱动程序中用于处理与控制器、 其根中心和所有终结点相关的操作。
-   UCX 对象创建的主机控制器驱动程序和每个对象的生存期由 UCX 管理。

**适用于**

-   Windows 10

**上次更新时间**

-   2015 年 7 月

**重要的 Api**

-   [**UcxControllerCreate**](https://msdn.microsoft.com/library/windows/hardware/mt188033)
-   [**UcxRootHubCreate**](https://msdn.microsoft.com/library/windows/hardware/mt188048)
-   [**UcxUsbDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/mt188052)

UCX 扩展了 WDF 对象功能来定义其自己特定于 USB 的 UCX 对象。 UCX 队列请求任何基础主机控制器驱动程序使用这些对象。

WDF 对象的更多详细信息，请参阅[Framework 对象简介](https://msdn.microsoft.com/library/windows/hardware/ff544249)。

## <a name="host-controller-object"></a>主机控制器对象


**UCXCONTROLLER**

表示创建的主机控制器驱动程序的主机控制器。 该驱动程序必须创建每个主机控制器实例只有一个主机控制器对象。 通常在中创建[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)通过调用回调[ **UcxControllerCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt188033)方法。

主机控制器驱动程序创建对象时，该驱动程序将注册其 UCX 由调用的回调函数的实现。 通过连接主机控制器，例如 ACPI 或 PCI 驱动程序此外可识别的总线类型。 该驱动程序还提供了主机控制器设备信息通过使用[ **UCX\_控制器\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/mt188057)结构传递给[ **UcxControllerCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt188033)调用。

若要处理 I/O 请求，主机控制器驱动程序必须注册一个 GUID\_DEVINTERFACE\_USB\_主机\_控制器设备接口。 该驱动程序不需要实现此接口中定义 Ioctl。 相反，UCX 客户端传递到 UCX 此接口上接收到通过调用 IOCTL 请求[ **UcxIoDeviceControl**](https://msdn.microsoft.com/library/windows/hardware/mt188047)。

下面是与主机控制器对象相关联 UCX 通过调用该回调函数。 这些函数必须由主机控制器驱动程序实现。

[*EVT\_UCX\_控制器\_USBDEVICE\_添加*](https://msdn.microsoft.com/library/windows/hardware/mt187823)  
当确定中心驱动程序，通过与根中心和/或外部的中心，新设备上存在的总线交互时调用。

[*EVT\_UCX\_控制器\_查询\_USB\_功能*](https://msdn.microsoft.com/library/windows/hardware/mt187821)  
调用由 UCX 来收集有关支持的 USB 主控制器的各种功能的信息。

[*EVT\_UCX\_控制器\_重置*](https://msdn.microsoft.com/library/windows/hardware/mt187822)  
由 UCX 重置可能中检测到错误响应的控制器硬件调用。

[*EVT\_UCX\_控制器\_获取\_当前\_FRAMENUMBER*](https://msdn.microsoft.com/library/windows/hardware/mt187820)  
用于从主控制器，计划同步传输中心驱动程序用于检索当前的帧数。

## <a name="root-hub-object"></a>根中心对象


**UCXROOTHUB**

获取并控制主控制器的根端口的状态。 通常在创建的主机控制器驱动程序[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)通过调用回调[ **UcxRootHubCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt188048)创建主机控制器对象后的方法。 应只有一个根中心对象，每个主机控制器实例。 在中**UcxRootHubCreate**调用时，该驱动程序注册其回调实现。

[*EVT\_UCX\_ROOTHUB\_GET\_INFO*](https://msdn.microsoft.com/library/windows/hardware/mt187836)  
返回数 USB 2.0 和 USB 3.0 端口根集线器。

[*EVT\_UCX\_ROOTHUB\_GET\_20PORT\_INFO*](https://msdn.microsoft.com/library/windows/hardware/mt187834)  
返回有关 USB 2.0 或 USB 3.0 端口的信息 ([*EVT\_UCX\_ROOTHUB\_获取\_30PORT\_信息*](https://msdn.microsoft.com/library/windows/hardware/mt187835)) 的根集线器。

创建并初始化根集线器对象后，中心驱动程序交互所使用的根集线器端口通过发送中断和控制传输。 UCX 协助这些传输通过调用由主机控制器驱动程序实现这些回调函数。

[*EVT\_UCX\_ROOTHUB\_控制\_URB*](https://msdn.microsoft.com/library/windows/hardware/mt187833)  
USB 集线器的处理功能控制请求。

[*EVT\_UCX\_ROOTHUB\_INTERRUPT\_TX*](https://msdn.microsoft.com/library/windows/hardware/mt187837)  
有关更改端口的信息的处理请求。

有关详细信息，请参阅[根主机控制器驱动程序的中心回调函数](manage-the-root-hub-in-a-host-controller-driver.md)。

## <a name="usb-device-object"></a>USB 设备对象


**UCXUSBDEVICE**

表示物理 USB 设备连接到总线。 通常在创建的主机控制器驱动程序[ *EVT\_UCX\_控制器\_USBDEVICE\_添加*](https://msdn.microsoft.com/library/windows/hardware/mt187823)通过调用回调[**UcxUsbDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt188052)方法。

创建对象后，主机控制器驱动程序注册的回调函数的实现[ **UcxUsbDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt188052)调用。

这些回调函数是为了使控制器和驱动程序通知有关 USB 设备的当前状态。

[*EVT\_UCX\_USBDEVICE\_ENABLE*](https://msdn.microsoft.com/library/windows/hardware/mt187841)  
准备执行传输到设备的默认终结点的控制器。

[*EVT\_UCX\_USBDEVICE\_DISABLE*](https://msdn.microsoft.com/library/windows/hardware/mt187840)  
释放与设备和其默认终结点相关联的控制器资源。

[*EVT\_UCX\_USBDEVICE\_ADDRESS*](https://msdn.microsoft.com/library/windows/hardware/mt187838)  
到控制器程序地址，并将发送一组\_地址传输到设备，以使其填好地址的状态。

[*EVT\_UCX\_USBDEVICE\_终结点\_配置*](https://msdn.microsoft.com/library/windows/hardware/mt187842)  
到控制器，程序的非默认终结点和/或释放其他非默认终结点。

[*EVT\_UCX\_USBDEVICE\_RESET*](https://msdn.microsoft.com/library/windows/hardware/mt187845)  
控制器通知，设备已被重置，这种情况下，驱动程序采用任何必要的操作与 USB 设备同步的控制器。

[*EVT\_UCX\_USBDEVICE\_UPDATE*](https://msdn.microsoft.com/library/windows/hardware/mt187846)  
通知控制器的多种与设备相关的信息。

[*EVT\_UCX\_USBDEVICE\_HUB\_INFO*](https://msdn.microsoft.com/library/windows/hardware/mt187844)  
通知中心属性，如果 UCXUSBDEVICE 处理是 hub 设备。

[*EVT\_UCX\_USBDEVICE\_ENDPOINT\_ADD*](https://msdn.microsoft.com/library/windows/hardware/mt187843)  
会通知驱动程序来创建设备的终结点。 [*EVT\_UCX\_USBDEVICE\_默认\_终结点\_添加*](https://msdn.microsoft.com/library/windows/hardware/mt187839)默认终结点。

当挂起的 USB 3.0 设备上某个接口具有向上信号唤醒时，驱动程序都应调用[ **UcxUsbDeviceRemoteWakeNotification** ](https://msdn.microsoft.com/library/windows/hardware/mt188054)通知 UCX。

创建对象后，该对象的生存期由 UCX，管理和驱动程序必须删除对象。

## <a name="endpoint-object"></a>终结点对象


**UCXENDPOINT**

表示一个 USB 设备对象上的终结点。 在由主机控制器创建终结点对象[ *EVT\_UCX\_USBDEVICE\_默认\_终结点\_添加*](https://msdn.microsoft.com/library/windows/hardware/mt187839)或[ *EVT\_UCX\_USBDEVICE\_终结点\_添加*](https://msdn.microsoft.com/library/windows/hardware/mt187843)回调。 创建终结点对象，该驱动程序将注册其回调函数。

该驱动程序还会创建 framework 队列对象的每个终结点，并通过调用将该队列的 WDFQUEUE 传递给 UCX [ **UcxEndpointSetWdfIoQueue**](https://msdn.microsoft.com/library/windows/hardware/mt188045)。 创建终结点后，该对象和其关联的队列的生存期由 UCX，管理和驱动程序必须删除这些对象本身。

该终结点对象实现多个允许驱动程序，以帮助 UCX 到终结点相关的操作的回调函数。

[*EVT\_UCX\_ENDPOINT\_ABORT*](https://msdn.microsoft.com/library/windows/hardware/mt187825)  
中止与终结点关联的队列。

[*EVT\_UCX\_ENDPOINT\_OK\_TO\_CANCEL\_TRANSFERS*](https://msdn.microsoft.com/library/windows/hardware/mt187826)  
通知控制器驱动程序，它可以完成取消终结点上的传输。

[*EVT\_UCX\_ENDPOINT\_PURGE*](https://msdn.microsoft.com/library/windows/hardware/mt187827)  
完成所有未完成的 I/O 请求的终结点上。

[*EVT\_UCX\_ENDPOINT\_START*](https://msdn.microsoft.com/library/windows/hardware/mt187829)  
启动与终结点关联的队列。

[*EVT\_UCX\_ENDPOINT\_STATIC\_STREAMS\_ADD*](https://msdn.microsoft.com/library/windows/hardware/mt187830)  
创建静态流。

[*EVT\_UCX\_ENDPOINT\_RESET*](https://msdn.microsoft.com/library/windows/hardware/mt187828)  
通知重置终结点的控制器的编程的驱动程序。

当主机控制器驱动程序收到一个终结点上的 USB 3.0 否 Ping 响应错误时，该驱动程序必须调用[ **UcxEndpointNoPingResponseError**](https://msdn.microsoft.com/library/windows/hardware/mt188043)。 USB 设备对象接收调用将导致[ *EVT\_UCX\_USBDEVICE\_更新*](https://msdn.microsoft.com/library/windows/hardware/mt187846)。
有关详细信息，请参阅[主机控制器驱动程序中的配置 USB 终结点](configuring-usb-endpoints-in-a-host-controller-driver.md)。

## <a name="stream-object"></a>Stream 对象


**UCXSTREAMS**

表示单个终结点设备的管道数。 主机控制器驱动程序创建中的流对象[ *EVT\_UCX\_终结点\_静态\_流\_添加*](https://msdn.microsoft.com/library/windows/hardware/mt187830)回调通过调用[ **UcxStaticStreamsCreate**](https://msdn.microsoft.com/library/windows/hardware/mt188050)。

期间[ **UcxStaticStreamsCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt188050)调用时，主机控制器驱动程序注册其回调函数。 对于特定的终结点对象，该驱动程序可以确定它是否已创建的流对象，并返回通过调用处理 UCXSTREAMS [ **UcxEndpointGetStaticStreamsReferenced**](https://msdn.microsoft.com/library/windows/hardware/mt188040)。

创建对象后，驱动程序创建的每个流 framework 队列对象，并通过调用将 WDFQUEUE 句柄发送到 UCX [ **UcxStaticStreamsSetStreamInfo**](https://msdn.microsoft.com/library/windows/hardware/mt188051)。

流对象提供了主控制器，以帮助 UCX 管理静态流的多个回调函数。

[*EVT\_UCX\_ENDPOINT\_STATIC\_STREAMS\_DISABLE*](https://msdn.microsoft.com/library/windows/hardware/mt187831)  
释放所有流终结点的控制器资源。

[*EVT\_UCX\_ENDPOINT\_STATIC\_STREAMS\_ENABLE*](https://msdn.microsoft.com/library/windows/hardware/mt187832)  
启用此终结点的所有流的控制器硬件。

对象和相关联的队列的生存期由 UCX，并且该驱动程序必须删除对象。

## <a name="related-topics"></a>相关主题
[为 USB 主控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)  



