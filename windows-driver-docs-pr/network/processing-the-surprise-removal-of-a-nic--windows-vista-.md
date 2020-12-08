---
title: 处理 NIC 意外删除 (Windows Vista)
description: 处理 NIC 意外删除 (Windows Vista)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecb5fb4bfc71c34284ea37ac780cc458592dc88e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822826"
---
# <a name="processing-the-surprise-removal-of-a-nic-windows-vista"></a>处理 NIC 意外删除 (Windows Vista)





以下步骤描述了 NDIS 如何在 Windows Vista 和 Windows Server 2008 中将 NIC 加入意外删除：

1.  PnP 管理器向 NIC 的设备堆栈发出 [**IRP \_ MN \_ 意外 \_ 删除**](../kernel/irp-mn-surprise-removal.md) 请求。

2.  当 NDIS 接收到此 IRP 时，它会调用连接到驱动程序堆栈中的 NIC 的最低筛选器驱动程序的 [*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event) 函数。 在此调用中，NDIS 指定了 **NetEventQueryRemoveDevice** 的事件代码。

    **注意**  NDIS 仅对播发 [*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event) 函数入口点的筛选器驱动程序执行此步骤。 筛选器驱动程序在调用 [**NdisFRegisterFilterDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver) 函数时播发此入口点。

     

3.  在对其 [*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event) 函数的调用上下文中，筛选器驱动程序必须调用 [**NdisFNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent) ，将 **NetEventQueryRemoveDevice** 事件向上转发到驱动程序堆栈中的下一个筛选器驱动程序。 这会导致 NDIS 使用 NetEventQueryRemoveDevice 的事件代码调用该筛选器驱动程序的 *FilterNetPnPEvent* 函数 **。**

    **注意**  NDIS 只为驱动程序堆栈中的下一个筛选器驱动程序执行此步骤，该驱动程序堆栈会公布 [*FilterNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event) 函数的入口点。

     

4.  驱动程序堆栈中的每个筛选器驱动程序重复上一步，直到堆栈中的最高筛选器驱动程序转发 **NetEventQueryRemoveDevice。** 事件。

    发生这种情况时，NDIS 会调用绑定到 NIC 的所有协议驱动程序的 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event) 函数。 在此调用中，NDIS 指定了 NetEventQueryRemoveDevice 的事件代码 **。**

5.  如果已成功初始化微型端口驱动程序，NDIS 将使用 **NdisDevicePnPEventSurpriseRemoved** 的事件代码调用 [*MiniportDevicePnPEventNotify*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)函数。 微型端口驱动程序应注意到设备已被物理删除。 如果微型端口驱动程序是 NDIS WDM 驱动程序，则应取消它向下发送到基础总线驱动程序的任何挂起的 Irp。 如果未成功初始化微型端口驱动程序，则继续处理。

6.  NDIS 将 IRP \_ MN \_ 意外 \_ 删除请求发送到堆栈中的下一个较低设备对象。 \_ \_ \_ 从堆栈中的下一个低设备对象收到返回的 IRP MN 意外删除请求后，NDIS 将完成 IRP \_ MN 的 \_ 意外 \_ 删除请求。

7.  PnP 管理器会发出 [**IRP \_ MN \_ remove \_ DEVICE**](../kernel/irp-mn-remove-device.md) 请求，以删除设备对象 (的软件表示形式，等等) NIC。

8.  NDIS 执行以下步骤：

    1.  它暂停绑定到 NIC 的所有协议驱动程序。

    2.  它将暂停附加到 NIC 的所有筛选器驱动程序。

    3.  它暂停 NIC 的微型端口驱动程序。

    4.  它调用绑定到 NIC 的所有协议驱动程序的 [*ProtocolUnbindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex) 函数。

    5.  它调用附加到 NIC 的所有筛选器模块的 [*FilterDetach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach) 函数。

9.  在所有协议和筛选器驱动程序未绑定并从 NIC 分离后，NDIS 将调用微型端口驱动程序的 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt) 函数。 NDIS 将 *MiniportHaltEx* 的 *HaltAction* 参数设置为 **NdisHaltDeviceSurpriseRemoved**。

10. NDIS 将 IRP \_ MN \_ REMOVE \_ device 请求发送到堆栈中的下一个较低设备对象。

11. 当 NDIS 接收到已完成的 IRP \_ MN \_ \_ 从堆栈中的下一个较低设备对象中删除设备请求时，ndis 会将功能设备 (对象销毁) 为 NIC 创建的 FDO。

 

