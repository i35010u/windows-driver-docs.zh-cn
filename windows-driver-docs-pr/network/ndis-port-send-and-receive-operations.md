---
title: NDIS 端口发送和接收操作
description: NDIS 端口发送和接收操作
keywords:
- 端口 WDK NDIS、发送和接收操作
- NDIS 端口 WDK、发送和接收操作
- 发送操作 WDK NDIS 端口
- 接收操作 WDK NDIS 端口
- 目标端口 WDK NDIS
- 源端口 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91fa919ff4d354ffefa242cc542ea0f7289462f2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801557"
---
# <a name="ndis-port-send-and-receive-operations"></a>NDIS 端口发送和接收操作





NDIS 驱动程序可以将发送和接收操作与 NDIS 端口关联起来。NDIS send 和 receive 函数的 *PortNumber* 参数中的端口号标识发送操作的目标端口或接收指示的源端口。 如果 *PortNumber* 为零，则使用默认端口。 当 NDIS 处理默认端口，而微型端口驱动程序未分配任何其他端口时，驱动程序堆栈中的任何 NDIS 驱动程序都不需要执行任何操作，始终将 *PortNumber* 参数设置为零。 有关在微型端口驱动程序中分配端口的详细信息，请参阅 [分配 NDIS 端口](allocating-an-ndis-port.md)。

如果微型端口驱动程序分配端口，则过量驱动程序可以使用这些端口来发送和接收关联微型端口适配器的相应 subinterfaces 上的数据。 但是，过量驱动程序必须确保端口处于活动状态，然后再发送任何数据。 当关联的 subinterfaces 可用时，微型端口驱动程序会激活端口。 有关激活微型端口驱动程序中的端口的详细信息，请参阅 [激活 NDIS 端口](activating-an-ndis-port.md)。

当 NDIS 调用协议驱动程序的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，ndis 会提供 *BindParameters* 参数指向的 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 **ActivePorts** 成员中所有当前活动端口的列表。 激活和停用端口时，NDIS 还会通知协议驱动程序具有 PnP 事件。 有关 PnP 端口激活和停用通知的详细信息，请参阅 [处理 NDIS 端口 PnP 通知](handling-ndis-ports-pnp-event-notifications.md)。 有关发送和接收操作的更多常规信息，请参阅 [发送和接收操作](send-and-receive-operations.md)。

 

