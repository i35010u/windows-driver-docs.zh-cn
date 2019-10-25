---
title: 启动 NIC
description: 启动 NIC
ms.assetid: 8463edba-1502-44b7-a9bd-30763b9e7679
keywords:
- Nic WDK 网络，开始
- 网络接口卡 WDK 网络，启动
- 即插即用 WDK NDIS 微型端口，开始 NIC
- 启动 Nic WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b23ebc59f1dd28c1f3e32535a2115cf9f9d403b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841833"
---
# <a name="starting-a-nic"></a>启动 NIC





以下步骤描述了 NDIS 如何参与 NIC 的开头：

1.  PnP 管理器颁发[**IRP\_MN\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。 此 IRP 包含的信息可通知 NDIS 有关 PnP 管理器已为 NIC 分配的资源。

2.  NDIS 设置[**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，并将 IRP\_MN\_启动\_设备请求向下传递到下一个最低的驱动程序，这通常是总线驱动程序。 当总线驱动程序收到 IRP\_MN\_开始\_设备请求时，总线驱动程序会在设备上执行其启动操作，并将已完成的 IRP\_MN\_启动\_设备请求备份设备堆栈。

3.  当 NDIS 接收到已完成的 IRP\_MN 时\_开始\_设备请求（即，当在所有较低版本的驱动程序使用 IRP 完成后，NDIS 的[**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程获得控制权），NDIS 将调用微型端口驱动程序[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数。

4.  如果*MiniportInitializeEx*函数返回 NDIS\_状态\_SUCCESS，ndis 会计划一个事件以调用所有协议驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数，这些驱动程序应绑定到该适配器，如注册表中的绑定信息。 请注意，微型端口驱动程序没有有关绑定的信息。

5.  NDIS 完成 IRP\_MN\_START\_设备请求。

 

 





