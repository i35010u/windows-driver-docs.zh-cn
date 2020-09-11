---
description: UCX 管理终结点对象的创建，并通知主机控制器将终结点编程或 deprogram 到 USB 主机控制器。
title: 在 USB 主控制器驱动程序中配置 USB 终结点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 177a63a2e71f873e0f492ff664ad5b977d53a86f
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010503"
---
# <a name="configure-usb-endpoints-in-a-usb-host-controller-driver"></a>在 USB 主控制器驱动程序中配置 USB 终结点


UCX 管理终结点对象的创建，并通知主机控制器将终结点编程或 deprogram 到 USB 主机控制器。

在对终结点进行编程时，它还由 UCX 进行管理。 当设备连接到总线并断开与总线的连接时，终结点的状态会发生变化，因此会经历关闭和重置等电源事件，并进行新的终结点创建（例如备用设置更改）。

## <a name="endpoint-configuration"></a>终结点配置


UCX 调用由主机控制器驱动程序实现的回调函数，以便在终结点必须编程到 USB 主机控制器或释放终结点时通知驱动程序。 如果调用了 [* \_ UCX \_ USBDEVICE \_ ENABLE*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_enable) ，则驱动程序会准备好控制器以执行到设备的默认终结点的传输。 准备控制器包括对默认终结点进行编程。 如果调用了 [*.Evt \_ UCX \_ USBDEVICE \_ DISABLE*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_disable) ，则驱动程序将 deprograms 默认终结点，并释放与该设备关联的其他控制器资源。 如果调用了 [* \_ UCX \_ USBDEVICE \_ 终结点 \_ 配置*](/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoints_configure) ，则会为驱动程序提供一个非默认终结点的列表，以将其引入控制器，并为其提供从控制器中移除的非默认终结点的另一个列表。 然后，主机控制器驱动程序会将指定的非默认终结点计划到控制器中，同时还会从控制器) 的其他列表中指定 (删除非默认终结点。

## <a name="queue-state-management"></a>队列状态管理


UCX 调用由主机控制器驱动程序实现的回调函数，以执行对终结点队列状态的更改。 然后，该驱动程序在提供给 UCX 的终结点队列上执行相应的操作，并在驱动程序中维护的任何二级队列上执行相应的操作。 在这些情况下，终结点队列将中止或清除：

-   USB 设备客户端驱动程序发送 URB \_ 函数 \_ 中止 \_ 管道请求。
-   挂起期间。
-   当设备连接到的中心时，将检测到设备断开连接。
-   在选择界面设置请求期间。

若要通知主机控制器驱动程序队列中止或清除，UCX 将调用 [*.Evt \_ UCX \_ 终结点 \_ 中止*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_abort) 或 [*.evt \_ UCX \_ 终结点 \_ 清除*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_purge)。 稍后，如果在某个时间点队列需要 UCX，则 UCX 将调用 [*.Evt \_ UCX \_ 终结点 \_ 启动*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_start) 回调以通知驱动程序启动队列。

## <a name="transfer-cancellation"></a>传输取消


对于主机控制器驱动程序 \_ \_ 在异步传输取消时声明 GUID USB 功能 \_ 明文 TT BUFFER 的任何控制器 \_ \_ \_ \_ \_ \_ ，驱动程序必须调用 [**UcxEndpointNeedToCancelTransfers**](/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointneedtocanceltransfers) 并实现 [*.evt \_ UCX \_ 终结点， \_ \_ 以 \_ 取消 \_ *](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers) 取消异步 (批量传输或控制) usb 传输到处于事务转换器 (TT) 集线器后面的 usb 完全或低速设备的传输。 在所有其他情况下，驱动程序可以选择调用 **UcxEndpointNeedToCancelTransfers** ，以获取一个在此终结点上允许取消传输的 * \_ UCX \_ 终结点 \_ \_ \_ \_ * ，然后驱动程序可以继续取消传输。 或者，驱动程序可以在不调用 **UcxEndpointNeedToCancelTransfers**的情况下直接取消传输。

如果主机控制器驱动程序始终无法对此 GUID 发出请求，则它可以完全忽略这两个函数调用。

如果驱动程序永远不会调用 [**UcxEndpointNeedToCancelTransfers**](/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointneedtocanceltransfers)，则不会调用驱动程序的 .Evt UCX 终结点，而不会调用该驱动程序的 [* \_ \_ 终结点 \_ \_ \_ \_ *](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers) 。

如果驱动程序打算使用 [**UcxEndpointNeedToCancelTransfers**](/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointneedtocanceltransfers)，则驱动程序必须调用方法，以便在将传输已编程到控制器然后取消，然后在完成传输之前等待 [*.Evt \_ UCX \_ 终结 \_ 点 \_ \_ 取消 \_ 传输*](/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers) 。

## <a name="related-topics"></a>相关主题
[为 USB 主控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)