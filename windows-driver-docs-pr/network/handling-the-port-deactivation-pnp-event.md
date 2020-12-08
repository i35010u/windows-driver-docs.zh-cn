---
title: 处理端口停用 PnP 事件
description: 处理端口停用 PnP 事件
keywords:
- 端口 WDK NDIS，PnP 事件通知
- NDIS 端口 WDK，PnP 事件通知
- PnP 事件通知 WDK NDIS 端口
- 停用 PnP 事件 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8b2475a2e73d3662cb8cec04980db5c64fa27b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821363"
---
# <a name="handling-the-port-deactivation-pnp-event"></a>处理端口停用 PnP 事件





当微型端口驱动程序停用 NDIS 端口时，过量驱动程序必须处理 **NetEventPortDeactivation** PnP 事件。 为了通知过量驱动程序的端口停用事件，NDIS 从基础微型端口驱动程序传播端口停用 PnP 事件。

在协议驱动程序完成端口停用 PnP 事件的处理之前，它必须确保与该端口关联的所有未完成的 OID 请求和发送请求均已完成。 协议驱动程序完成 PnP 事件之后，驱动程序必须确保不会为该端口发出任何 OID 请求或发送请求。

微型端口驱动程序指定 [**NET \_ pnp \_ 事件 \_ 通知**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)结构中的 **NetEventPortDeactivation** PnP 事件代码， *NetPnPEvent* 参数在调用 [**NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)函数时指向该代码，以报告某些端口已停用。 微型端口驱动程序指定一个 NDIS \_ 端口 \_ 号值的数组，以列出停用的端口。 有关端口号数组的详细信息，请参阅 [停用 NDIS 端口](deactivating-an-ndis-port.md)。

 

