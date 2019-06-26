---
title: 移除 NIC
description: 移除 NIC
ms.assetid: eaa4b784-4375-465d-9ef5-99b38b7fd15a
keywords:
- Nic WDK 连接网络、 删除
- 网络接口卡 WDK 连接网络、 删除
- 即插即用 WDK NDIS 微型端口，删除 NIC
- 删除 Nic WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b896870ebb2502f9e5a52e7b3b74766e1b6823f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385836"
---
# <a name="removing-a-nic"></a>移除 NIC





以下步骤介绍如何 NDIS 参与删除的 NIC:

1.  即插即用 manager 问题[ **IRP\_MN\_查询\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)是否 NIC 可以删除而不会中断对查询的请求计算机。

2.  当 NDIS 接收此 IRP 时，它将调用[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)附加到的 NIC 驱动程序堆栈中的最小筛选器驱动程序的函数。 NDIS 此调用中指定的事件代码**NetEventQueryRemoveDevice**。

    **请注意**  NDIS 执行此步骤中，仅对播发条目的筛选器驱动程序，为点[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)函数。 筛选器驱动程序将公布此入口点时它将调用[ **NdisFRegisterFilterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfregisterfilterdriver)函数。

     

3.  对调用的上下文中其[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)函数，筛选器驱动程序必须调用[ **NdisFNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfnetpnpevent)转发**NetEventQueryRemoveDevice**事件传送至驱动程序堆栈中的下一个筛选器驱动程序。 这将导致调用该筛选器驱动程序的 NDIS *FilterNetPnPEvent*函数的事件代码**NetEventQueryRemoveDevice**。

    **请注意**  NDIS 仅对播发的入口点的驱动程序堆栈中的下一个筛选器驱动程序执行此步骤[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)函数。

     

4.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中最高的筛选器驱动程序已转发**NetEventQueryRemoveDevice**事件。

    当发生这种情况，将调用 NDIS [ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)函数绑定到 NIC 的所有协议驱动程序 NDIS 此调用中指定的事件代码**NetEventQueryRemoveDevice**。

5.  如果协议驱动程序失败**NetEventQueryRemoveDevice**事件通过返回失败代码 NDIS\_状态\_发生故障*ProtocolNetPnPEvent*，NDIS 或 PnP 管理器可能会忽略错误并随之成功[ **IRP\_MN\_查询\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)请求。 协议驱动程序因此，必须准备好处理删除的 NIC，即使协议驱动程序失败**NetEventQueryRemoveDevice**事件。

6.  即插即用 manager 问题[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求要删除的 NIC 或软件表示形式（设备对象等）[**IRP\_MN\_取消\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)取消挂起的删除请求。 请注意，IRP\_MN\_删除\_设备的请求始终前面没有 IRP\_MN\_查询\_删除\_设备的请求。

7.  如果 PnP 管理器将发出 IRP\_MN\_取消\_删除\_设备请求、 NDIS 调用[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)的最小的函数附加到的 NIC 驱动程序堆栈中的筛选器驱动程序。 NDIS 此调用中指定的事件代码**NetEventCancelRemoveDevice**。

    **请注意**  NDIS 执行此步骤中，仅对播发条目的筛选器驱动程序，为点[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)函数。

     

8.  对调用的上下文中其[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)函数，筛选器驱动程序必须调用[ **NdisFNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfnetpnpevent)转发**NetEventCancelRemoveDevice**事件传送至驱动程序堆栈中的下一个筛选器驱动程序。 这将导致调用该筛选器驱动程序的 NDIS *FilterNetPnPEvent*函数的事件代码**NetEventCancelRemoveDevice**。

    **请注意**  NDIS 仅对播发的入口点的驱动程序堆栈中的下一个筛选器驱动程序执行此步骤[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)函数。

     

9.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中最高的筛选器驱动程序已转发**NetEventCancelRemoveDevice**事件。

    当发生这种情况，将调用 NDIS [ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)函数绑定到 NIC 的所有协议驱动程序 NDIS 此调用中指定的事件代码**NetEventCancelRemoveDevice**。 此事件代码结束处删除序列。

10. 如果 PnP 管理器将发出 IRP\_MN\_删除\_设备请求，NDIS 会执行以下步骤：

    1.  它将暂停所有协议驱动程序绑定到 nic。

    2.  附加到 NIC 的所有筛选器驱动程序，它将暂停

    3.  微型端口驱动程序的 NIC，它将暂停

    4.  它将调用[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)函数绑定到 NIC 的所有协议驱动程序

    5.  它将调用[ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)附加到 NIC 的所有筛选器模块的函数

11. NDIS 微型端口驱动程序已成功初始化，如果调用微型端口驱动程序[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数。 NDIS 集*HaltAction*的参数*MiniportHaltEx*到**NdisHaltDeviceDisabled**。

12. NDIS 发送 IRP\_MN\_删除\_设备请求到堆栈中较低的下一个设备对象。

13. 当 NDIS 收到已完成的 IRP\_MN\_删除\_从下一个较低的设备的设备请求对象在堆栈中 NDIS 销毁功能的设备对象 (FDO) 创建的 nic。

 

 





