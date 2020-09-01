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
ms.openlocfilehash: 4df55ffba133ee6763a3c6426fbf982425819354
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217519"
---
# <a name="removing-a-nic"></a>移除 NIC





以下步骤描述了 NDIS 如何参与删除 NIC：

1.  PnP 管理器发出 [**IRP \_ MN \_ 查询 \_ 删除 \_ 设备**](../kernel/irp-mn-query-remove-device.md) 请求，查询是否可以在不中断计算机的情况下删除该 NIC。

2.  当 NDIS 接收到此 IRP 时，它会调用连接到驱动程序堆栈中的 NIC 的最低筛选器驱动程序的 [*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event) 函数。 在此调用中，NDIS 指定了 **NetEventQueryRemoveDevice**的事件代码。

    **注意**   NDIS 仅对播发[*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数入口点的筛选器驱动程序执行此步骤。 筛选器驱动程序在调用 [**NdisFRegisterFilterDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver) 函数时公布此入口点。

     

3.  在对其 [*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event) 函数的调用上下文中，筛选器驱动程序必须调用 [**NdisFNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent) ，将 **NetEventQueryRemoveDevice** 事件向上转发到驱动程序堆栈中的下一个筛选器驱动程序。 这会导致 NDIS 使用**NetEventQueryRemoveDevice**的事件代码调用该筛选器驱动程序的*FilterNetPnPEvent*函数。

    **注意**   NDIS 只为驱动程序堆栈中的下一个筛选器驱动程序执行此步骤，该驱动程序堆栈会公布[*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数的入口点。

     

4.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中的最高筛选器驱动程序转发了 **NetEventQueryRemoveDevice** 事件。

    发生这种情况时，NDIS 会调用绑定到 NIC 的所有协议驱动程序的 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event) 函数。 在此调用中，NDIS 指定了 **NetEventQueryRemoveDevice**的事件代码。

5.  如果协议驱动程序通过返回失败代码 "ProtocolNetPnPEvent" 中的 "NDIS 状态失败" 导致**NetEventQueryRemoveDevice**事件失败 \_ \_ ，ndis 或 PnP 管理器可能会忽略该错误，然后成功完成[**IRP \_ MN \_ 查询 " \_ 删除 \_ 设备**](../kernel/irp-mn-query-remove-device.md)请求"。 *ProtocolNetPnPEvent* 因此，协议驱动程序必须准备好处理 NIC 的删除操作，即使协议驱动程序无法 **NetEventQueryRemoveDevice** 事件。

6.  PnP 管理器发出 [**IRP \_ MN \_ remove \_ device**](../kernel/irp-mn-remove-device.md) 请求以删除设备对象 (的软件表示形式，等等) NIC 或 [**IRP \_ MN \_ 取消 \_ 删除 \_ 设备**](../kernel/irp-mn-cancel-remove-device.md) 请求来取消挂起的删除。 请注意，IRP \_ MN \_ 删除 \_ 设备请求并非始终在 irp \_ MN \_ 查询 \_ 删除 \_ 设备请求之前。

7.  如果 PnP 管理器发出 IRP \_ MN \_ CANCEL \_ REMOVE \_ DEVICE 请求，NDIS 将调用连接到驱动程序堆栈中的 NIC 的最低筛选器驱动程序的 [*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event) 函数。 在此调用中，NDIS 指定了 **NetEventCancelRemoveDevice**的事件代码。

    **注意**   NDIS 仅对播发[*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数入口点的筛选器驱动程序执行此步骤。

     

8.  在对其 [*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event) 函数的调用上下文中，筛选器驱动程序必须调用 [**NdisFNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent) ，将 **NetEventCancelRemoveDevice** 事件向上转发到驱动程序堆栈中的下一个筛选器驱动程序。 这会导致 NDIS 使用**NetEventCancelRemoveDevice**的事件代码调用该筛选器驱动程序的*FilterNetPnPEvent*函数。

    **注意**   NDIS 只为驱动程序堆栈中的下一个筛选器驱动程序执行此步骤，该驱动程序堆栈会公布[*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)函数的入口点。

     

9.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中的最高筛选器驱动程序转发了 **NetEventCancelRemoveDevice** 事件。

    发生这种情况时，NDIS 会调用绑定到 NIC 的所有协议驱动程序的 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event) 函数。 在此调用中，NDIS 指定了 **NetEventCancelRemoveDevice**的事件代码。 此事件代码将结束删除序列。

10. 如果 PnP 管理器发出 IRP \_ MN \_ REMOVE \_ 设备请求，NDIS 将执行以下步骤：

    1.  它暂停绑定到 NIC 的所有协议驱动程序。

    2.  它将暂停附加到 NIC 的所有筛选器驱动程序。

    3.  它暂停 NIC 的微型端口驱动程序。

    4.  它调用绑定到 NIC 的所有协议驱动程序的 [*ProtocolUnbindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex) 函数。

    5.  它调用附加到 NIC 的所有筛选器模块的 [*FilterDetach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach) 函数。

11. 如果已成功初始化微型端口驱动程序，NDIS 将调用微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数。 NDIS 将*MiniportHaltEx*的*HaltAction*参数设置为**NdisHaltDeviceDisabled**。

12. NDIS 将 IRP \_ MN \_ REMOVE \_ device 请求发送到堆栈中的下一个较低设备对象。

13. 当 NDIS 接收到已完成的 IRP \_ MN \_ \_ 从堆栈中的下一个较低设备对象中删除设备请求时，ndis 会将功能设备 (对象销毁) 为 NIC 创建的 FDO。

 

