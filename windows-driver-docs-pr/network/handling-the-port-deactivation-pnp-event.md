---
title: 处理端口停用 PnP 事件
description: 处理端口停用 PnP 事件
ms.assetid: 0e3b10a7-5ab5-48e1-a5cc-c7bc6ce26410
keywords:
- 端口 WDK NDIS，PnP 事件通知
- NDIS 端口 WDK，PnP 事件通知
- PnP 事件通知 WDK NDIS 端口
- 停用 PnP 事件 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d60f2dc7d64eb9bd6d44b465295ace0f2a9ed7a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842551"
---
# <a name="handling-the-port-deactivation-pnp-event"></a>处理端口停用 PnP 事件





当微型端口驱动程序停用 NDIS 端口时，过量驱动程序必须处理**NetEventPortDeactivation** PnP 事件。 为了通知过量驱动程序的端口停用事件，NDIS 从基础微型端口驱动程序传播端口停用 PnP 事件。

在协议驱动程序完成端口停用 PnP 事件的处理之前，它必须确保与该端口关联的所有未完成的 OID 请求和发送请求均已完成。 协议驱动程序完成 PnP 事件之后，驱动程序必须确保不会为该端口发出任何 OID 请求或发送请求。

微型端口驱动程序指定[**NET\_pnp\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)中的**NetEventPortDeactivation** PNP 事件代码\_通知结构， *NetPnPEvent*参数在调用[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)用于报告某些端口已停用的函数。 微型端口驱动程序指定一个 NDIS\_端口的数组，\_NUMBER 值列出已停用的端口。 有关端口号数组的详细信息，请参阅[停用 NDIS 端口](deactivating-an-ndis-port.md)。

 

 





