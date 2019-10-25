---
title: 移除 NIC
description: 移除 NIC
ms.assetid: eaa4b784-4375-465d-9ef5-99b38b7fd15a
keywords:
- Nic WDK 网络，删除
- 网络接口卡 WDK 网络，删除
- 即插即用 WDK NDIS 微型端口，删除 NIC
- 删除 Nic WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 157c2499cbec6f322ffe09aed2faecd6480801b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842069"
---
# <a name="removing-a-nic"></a>移除 NIC





以下步骤描述了 NDIS 如何参与删除 NIC：

1.  PnP 管理器颁发[**IRP\_MN\_query\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)请求，查询是否可以在不中断计算机的情况下删除该 NIC。

2.  当 NDIS 接收到此 IRP 时，它会调用连接到驱动程序堆栈中的 NIC 的最低筛选器驱动程序的[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数。 在此调用中，NDIS 指定了**NetEventQueryRemoveDevice**的事件代码。

    **请注意**  NDIS 仅对播发[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数入口点的筛选器驱动程序执行此步骤。 筛选器驱动程序在调用[**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)函数时公布此入口点。

     

3.  在对其[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数的调用上下文中，筛选器驱动程序必须调用[**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent) ，将**NetEventQueryRemoveDevice**事件向上转发到驱动程序堆栈中的下一个筛选器驱动程序。 这会导致 NDIS 使用**NetEventQueryRemoveDevice**的事件代码调用该筛选器驱动程序的*FilterNetPnPEvent*函数。

    **请注意**  NDIS 只为驱动程序堆栈中的下一个筛选器驱动程序执行此步骤，该驱动程序堆栈会公布[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数的入口点。

     

4.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中的最高筛选器驱动程序转发了**NetEventQueryRemoveDevice**事件。

    发生这种情况时，NDIS 会调用绑定到 NIC 的所有协议驱动程序的[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)函数。 在此调用中，NDIS 指定了**NetEventQueryRemoveDevice**的事件代码。

5.  如果协议驱动程序在**NetEventQueryRemoveDevice**事件失败的情况下返回失败代码 NDIS\_状态\_从*ProtocolNetPnPEvent*失败，ndis 或 PnP 管理器可能会忽略该错误，并随后成功[**IRP\_MN\_查询\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)请求。 因此，协议驱动程序必须准备好处理 NIC 的删除操作，即使协议驱动程序无法**NetEventQueryRemoveDevice**事件。

6.  PnP 管理器发出[**IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求以删除 NIC 或[**IRP\_MN\_取消\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)的软件表示（设备对象等）请求取消挂起的删除。 请注意，IRP\_MN\_删除\_设备请求并非始终以 IRP\_MN\_查询为前缀，\_删除\_设备请求。

7.  如果 PnP 管理器颁发 IRP\_MN\_CANCEL\_删除\_设备请求，NDIS 将调用连接到驱动程序堆栈中的 NIC 的最低筛选器驱动程序的[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数。 在此调用中，NDIS 指定了**NetEventCancelRemoveDevice**的事件代码。

    **请注意**  NDIS 仅对播发[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数入口点的筛选器驱动程序执行此步骤。

     

8.  在对其[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数的调用上下文中，筛选器驱动程序必须调用[**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent) ，将**NetEventCancelRemoveDevice**事件向上转发到驱动程序堆栈中的下一个筛选器驱动程序。 这会导致 NDIS 使用**NetEventCancelRemoveDevice**的事件代码调用该筛选器驱动程序的*FilterNetPnPEvent*函数。

    **请注意**  NDIS 只为驱动程序堆栈中的下一个筛选器驱动程序执行此步骤，该驱动程序堆栈会公布[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数的入口点。

     

9.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中的最高筛选器驱动程序转发了**NetEventCancelRemoveDevice**事件。

    发生这种情况时，NDIS 会调用绑定到 NIC 的所有协议驱动程序的[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)函数。 在此调用中，NDIS 指定了**NetEventCancelRemoveDevice**的事件代码。 此事件代码将结束删除序列。

10. 如果 PnP 管理器颁发 IRP\_MN\_删除\_设备请求，NDIS 会执行以下步骤：

    1.  它暂停绑定到 NIC 的所有协议驱动程序。

    2.  它将暂停附加到 NIC 的所有筛选器驱动程序。

    3.  它暂停 NIC 的微型端口驱动程序。

    4.  它调用绑定到 NIC 的所有协议驱动程序的[*ProtocolUnbindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)函数。

    5.  它调用附加到 NIC 的所有筛选器模块的[*FilterDetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)函数。

11. 如果已成功初始化微型端口驱动程序，NDIS 将调用微型端口驱动程序的[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)函数。 NDIS 将*MiniportHaltEx*的*HaltAction*参数设置为**NdisHaltDeviceDisabled**。

12. NDIS 将 IRP\_MN 发送\_删除\_设备请求发送到堆栈中的下一个较低设备对象。

13. 当 NDIS 接收到完成的 IRP\_MN\_从堆栈中的下一个较低设备对象中删除\_设备请求，NDIS 会销毁为 NIC 创建的功能设备对象（FDO）。

 

 





