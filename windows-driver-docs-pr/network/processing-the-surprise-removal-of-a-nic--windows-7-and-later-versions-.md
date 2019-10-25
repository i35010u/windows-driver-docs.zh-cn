---
title: 处理对 NIC 的意外删除（Windows 7 和更高版本）
description: 处理 NIC 意外删除（Windows 7 和更高版本）
ms.assetid: D1C1C862-8AFF-490F-8A1D-362280196548
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cff6dbf4cc777cb633af02882d9f515a818ea05
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843482"
---
# <a name="processing-the-surprise-removal-of-a-nic-windows-7-and-later-versions"></a>处理 NIC 意外删除（Windows 7 和更高版本）





在 Windows 7 和 Windows Server 2008 R2 及更高版本中，NDIS 可能会与以前版本的 Windows 中的网络接口卡（NIC）意外删除。 如果满足以下*任一*条件，NDIS 会执行修改后的意外删除过程：

-   操作系统为 Windows 8/Windows Server 2012 或更高版本。
-   操作系统为 Windows 7，并且已安装 KB2471472 的修补程序。
-   操作系统为 Windows 7，网络适配器是移动宽带（MBB）设备。

如果未满足上述任何条件，NDIS 就会像在以前版本的 Windows 中那样参与意外删除过程。 有关此过程的详细信息，请参阅[处理 NIC （Windows Vista）的意外删除](processing-the-surprise-removal-of-a-nic--windows-vista-.md)。

以下步骤描述了 NDIS 加入 NIC 的意外删除的修订方式：

1.  PnP 管理器发出[**IRP\_MN\_将\_删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)请求发送到 NIC 的设备堆栈。

2.  当 NDIS 接收到此 IRP 时，它会调用连接到驱动程序堆栈中的 NIC 的最低筛选器驱动程序的[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数。 在此调用中，NDIS 指定了**NetEventQueryRemoveDevice**的事件代码。

    **请注意**  NDIS 仅对播发[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数入口点的筛选器驱动程序执行此步骤。 筛选器驱动程序在调用[**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)函数时播发此入口点。

     

3.  在对其[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数的调用上下文中，筛选器驱动程序必须调用[**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent) ，将**NetEventQueryRemoveDevice**事件向上转发到驱动程序堆栈中的下一个筛选器驱动程序。 这会导致 NDIS 使用**NetEventQueryRemoveDevice**的事件代码调用该筛选器驱动程序的*FilterNetPnPEvent*函数。

    **请注意**  NDIS 只为驱动程序堆栈中的下一个筛选器驱动程序执行此步骤，该驱动程序堆栈会公布[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数的入口点。

     

4.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中的最高筛选器驱动程序转发了**NetEventQueryRemoveDevice**事件。

    发生这种情况时，NDIS 会调用绑定到 NIC 的所有协议驱动程序的[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)函数。 在此调用中，NDIS 指定了**NetEventQueryRemoveDevice**的事件代码。

5.  NDIS 使用**NdisDevicePnPEventSurpriseRemoved**的事件代码调用[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)函数。 微型端口驱动程序应注意到设备已被物理删除。 如果微型端口驱动程序是 NDIS WDM 驱动程序，则应取消它向下发送到基础总线驱动程序的任何挂起的 Irp。

6.  NDIS 执行以下步骤：

    1.  它暂停绑定到 NIC 的所有协议驱动程序。

    2.  它将暂停附加到 NIC 的所有筛选器驱动程序。

    3.  它暂停 NIC 的微型端口驱动程序。

    4.  它调用绑定到 NIC 的所有协议驱动程序的[*ProtocolUnbindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)函数。

    5.  它调用附加到 NIC 的所有筛选器模块的[*FilterDetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)函数。

7.  在所有协议和筛选器驱动程序未绑定并从 NIC 分离后，NDIS 将调用微型端口驱动程序的[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数。 NDIS 将*MiniportHaltEx*的*HaltAction*参数设置为**NdisHaltDeviceSurpriseRemoved**。

8.  NDIS 将 IRP\_MN\_意外\_删除请求发送到堆栈中的下一个较低设备对象。 接收到返回的 IRP 之后\_MN\_从堆栈中的下一个较低设备对象意外\_删除请求，NDIS 将完成 IRP\_MN\_删除请求。

9.  PnP 管理器颁发[**IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求，删除 NIC 的软件表示（设备对象等）。

10. NDIS 将 IRP\_MN 发送\_删除\_设备请求发送到堆栈中的下一个较低设备对象。

11. 当 NDIS 接收到完成的 IRP\_MN\_从堆栈中的下一个较低设备对象中删除\_设备请求，NDIS 会销毁为 NIC 创建的功能设备对象（FDO）。

 

 





