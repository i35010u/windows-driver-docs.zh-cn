---
title: NDIS 端口发送和接收操作
description: NDIS 端口发送和接收操作
ms.assetid: f9a22b7b-5565-4d56-a9b9-22562b6bf0da
keywords:
- 端口 WDK NDIS、发送和接收操作
- NDIS 端口 WDK、发送和接收操作
- 发送操作 WDK NDIS 端口
- 接收操作 WDK NDIS 端口
- 目标端口 WDK NDIS
- 源端口 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dfff928c0a682fbc6b27606c65beab01c0c4009
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826949"
---
# <a name="ndis-port-send-and-receive-operations"></a>NDIS 端口发送和接收操作





NDIS 驱动程序可以将发送和接收操作与 NDIS 端口关联起来。NDIS send 和 receive 函数的*PortNumber*参数中的端口号标识发送操作的目标端口或接收指示的源端口。 如果*PortNumber*为零，则使用默认端口。 当 NDIS 处理默认端口，而微型端口驱动程序未分配任何其他端口时，驱动程序堆栈中的任何 NDIS 驱动程序都不需要执行任何操作，始终将*PortNumber*参数设置为零。 有关在微型端口驱动程序中分配端口的详细信息，请参阅[分配 NDIS 端口](allocating-an-ndis-port.md)。

如果微型端口驱动程序分配端口，则过量驱动程序可以使用这些端口来发送和接收关联微型端口适配器的相应 subinterfaces 上的数据。 但是，过量驱动程序必须确保端口处于活动状态，然后再发送任何数据。 当关联的 subinterfaces 可用时，微型端口驱动程序会激活端口。 有关激活微型端口驱动程序中的端口的详细信息，请参阅[激活 NDIS 端口](activating-an-ndis-port.md)。

当 NDIS 调用协议驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，Ndis 在[**ndis\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 *ActivePorts 成员中提供了所有当前处于活动状态的端口的列表，BindParameters*参数指向。 激活和停用端口时，NDIS 还会通知协议驱动程序具有 PnP 事件。 有关 PnP 端口激活和停用通知的详细信息，请参阅[处理 NDIS 端口 PnP 通知](handling-ndis-ports-pnp-event-notifications.md)。 有关发送和接收操作的更多常规信息，请参阅[发送和接收操作](send-and-receive-operations.md)。

 

 





