---
Description: UCX 管理终结点对象的创建，并通知主机控制器将终结点编程或 deprogram 到 USB 主机控制器。
title: 在 USB 主控制器驱动程序中配置 USB 终结点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4fda14fc82d162337d8f87f0e007fbb0ec91e35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842401"
---
# <a name="configure-usb-endpoints-in-a-usb-host-controller-driver"></a>在 USB 主控制器驱动程序中配置 USB 终结点


UCX 管理终结点对象的创建，并通知主机控制器将终结点编程或 deprogram 到 USB 主机控制器。

在对终结点进行编程时，它还由 UCX 进行管理。 当设备连接到总线并断开与总线的连接时，终结点的状态会发生变化，因此会经历关闭和重置等电源事件，并进行新的终结点创建（例如备用设置更改）。

## <a name="endpoint-configuration"></a>终结点配置


UCX 调用由主机控制器驱动程序实现的回调函数，以便在终结点必须编程到 USB 主机控制器或释放终结点时通知驱动程序。 如果调用的是[ *\_UCX\_USBDEVICE\_ENABLE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_enable) ，则驱动程序将准备用于执行到设备默认终结点的传输的控制器。 准备控制器包括对默认终结点进行编程。 如果调用的是[ *\_UCX\_USBDEVICE\_DISABLE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_disable) ，则驱动程序将 deprograms 默认终结点并释放与该设备关联的其他控制器资源。 如果调用的是[ *\_UCX\_USBDEVICE\_终结\_点*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoints_configure)，则会为驱动程序提供一个非默认终结点的列表，以将程序引入到控制器中，并从控制器. 然后，主机控制器驱动程序将指定的非默认终结点计划到控制器中，同时从控制器中删除非默认终结点（在另一个列表中指定）。

## <a name="queue-state-management"></a>队列状态管理


UCX 调用由主机控制器驱动程序实现的回调函数，以执行对终结点队列状态的更改。 然后，该驱动程序在提供给 UCX 的终结点队列上执行相应的操作，并在驱动程序中维护的任何二级队列上执行相应的操作。 在这些情况下，终结点队列将中止或清除：

-   USB 设备客户端驱动程序\_中止\_管道请求发送 URB\_函数。
-   挂起期间。
-   当设备连接到的中心时，将检测到设备断开连接。
-   在选择界面设置请求期间。

若要通知主机控制器驱动程序有关队列中止或清除的信息，UCX 会[ *\_调用\_终结点\_中止*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_abort)或[ *.evt\_UCX\_终结点\_清除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_purge)的。 稍后，如果在某个时间点队列需要 UCX，则 UCX 将[ *\_终结点\_"启动*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_start)回叫" 来调用\_该 UCX，以通知驱动程序启动队列。

## <a name="transfer-cancellation"></a>传输取消


对于主机控制器驱动程序声明 GUID\_USB\_功能的任何控制器\_明文\_TT\_缓存\_，驱动程序必须调用[**UcxEndpointNeedToCancelTransfers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointneedtocanceltransfers)并实现[ *\_UCX\_终结点\_"确定"\_，以\_取消取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers)异步（批量或控制） USB传输到事务转换器（TT）中心后面的 USB 全速或低速设备。 在所有其他情况下，驱动程序可以选择调用**UcxEndpointNeedToCancelTransfers** ，以获取一个 *\_UCX\_终结点\_"确定"\_\_"取消"\_* 此终结点允许传输，驱动程序可以继续取消传输。 或者，驱动程序可以在不调用**UcxEndpointNeedToCancelTransfers**的情况下直接取消传输。

如果主机控制器驱动程序始终无法对此 GUID 发出请求，则它可以完全忽略这两个函数调用。

如果驱动程序永远不会调用[**UcxEndpointNeedToCancelTransfers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointneedtocanceltransfers)，则驱动程序的[ *.evt\_UCX\_终结点\_"确定"\_为\_"取消"* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers) 。报名.

如果驱动程序打算使用[**UcxEndpointNeedToCancelTransfers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointneedtocanceltransfers)，则驱动程序必须调用方法，以便在将传输已编程到控制器然后取消，然后等待[ *\_UCX\_终结点\_"确定"\_若要\_在完成前取消\_传输*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers)。

## <a name="related-topics"></a>相关主题
[为 USB 主控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)  



