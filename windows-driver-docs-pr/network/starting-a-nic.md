---
title: 启动 NIC
description: 启动 NIC
ms.assetid: 8463edba-1502-44b7-a9bd-30763b9e7679
keywords:
- Nic WDK 网络启动
- 网络接口卡 WDK 网络启动
- 即插即用 WDK NDIS 微型端口，启动 NIC
- 起始 Nic WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34b8b932b021ab2d59fde24fe91a5746c031e6b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377558"
---
# <a name="starting-a-nic"></a>启动 NIC





以下步骤介绍如何 NDIS 加入 NIC 的开始：

1.  即插即用 manager 问题[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。 此 IRP 包含 NDIS 告知 PnP 管理器已为 NIC 分配的资源的信息

2.  NDIS 集[ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程并将 IRP\_MN\_启动\_到下一个最低驱动程序，这通常是在设备堆栈的下层设备请求总线驱动程序。 当总线驱动程序接收 IRP\_MN\_启动\_设备请求，总线驱动程序执行其在设备上的启动操作，并且将已完成的 IRP\_MN\_启动\_设备请求备份设备堆栈。

3.  当 NDIS 收到已完成的 IRP\_MN\_启动\_设备的请求 (即，当 NDIS 的[ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程者控制了所有较低的驱动程序用完 IRP），NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。

4.  如果*MiniportInitializeEx*函数将返回 NDIS\_状态\_成功后，NDIS 计划事件来调用[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数都将绑定到适配器，因此认为由注册表中的绑定信息的所有协议驱动程序。 请注意，微型端口驱动程序绑定的任何信息。

5.  NDIS 完成 IRP\_MN\_启动\_设备的请求。

 

 





