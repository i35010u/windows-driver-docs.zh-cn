---
title: 启动 NIC
description: 启动 NIC
keywords:
- Nic WDK 网络，开始
- 网络接口卡 WDK 网络，启动
- 即插即用 WDK NDIS 微型端口，开始 NIC
- 启动 Nic WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d229270dfb733bc3dc015c82b0f286a441a86712
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801267"
---
# <a name="starting-a-nic"></a>启动 NIC





以下步骤描述了 NDIS 如何参与 NIC 的开头：

1.  PnP 管理器颁发 [**IRP \_ MN \_ 启动 \_ 设备**](../kernel/irp-mn-start-device.md) 请求。 此 IRP 包含的信息可通知 NDIS 有关 PnP 管理器已为 NIC 分配的资源。

2.  NDIS 设置 [**IoCompletion**](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，并将 IRP \_ MN \_ START \_ device 请求按设备堆栈向下传递到下一个最低的驱动程序，该驱动程序通常是总线驱动程序。 当总线驱动程序收到 IRP \_ MN \_ start \_ 设备请求时，总线驱动程序会在设备上执行其启动操作，并将已完成的 IRP \_ MN \_ 启动设备请求传递到 \_ 设备堆栈。

3.  当 NDIS 接收到完成的 IRP \_ MN \_ START \_ DEVICE 请求 (即，当在所有较低版本的驱动程序都已完成 irp) 的情况下，ndis 的 [**DispatchPnP**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程会获得控制权，ndis 将调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数。

4.  如果 *MiniportInitializeEx* 函数返回 NDIS \_ 状态 \_ SUCCESS，ndis 会计划一个事件以调用所有协议驱动程序的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex) 函数，这些驱动程序应绑定到适配器，如注册表中的绑定信息所示。 请注意，微型端口驱动程序没有有关绑定的信息。

5.  NDIS 完成 IRP \_ MN \_ 启动 \_ 设备请求。

 

