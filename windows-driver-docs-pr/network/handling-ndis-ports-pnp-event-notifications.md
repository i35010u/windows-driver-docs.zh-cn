---
title: NDIS 端口 PnP 事件通知
description: NDIS 端口 PnP 事件通知
keywords:
- 端口 WDK NDIS，PnP 事件通知
- NDIS 端口 WDK，PnP 事件通知
- PnP 事件通知 WDK NDIS 端口
- 事件通知 WDK 网络
- 通知 WDK 网络
- 通知 WDK PnP，NDIS 端口
- 事件 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97c101bd2bf7991a3815cbe2453721159fe34993
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787267"
---
# <a name="ndis-ports-pnp-event-notifications"></a>NDIS 端口 PnP 事件通知

当激活或停用端口时，NDIS 转发 PnP 事件以通知过量驱动程序。 分配端口时，NDIS 和微型端口驱动程序不会生成 PnP 事件。 微型端口驱动程序通知 NDIS：已使用 **NetEventPortActivation** PnP 事件激活端口，微型端口驱动程序生成 **NetEventPortDeactivation** PnP 事件，以通知 NDIS，某些端口已被停用。

当 NDIS 调用协议驱动程序的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，Ndis 在 *BindParameters* 参数的 [**Ndis \_ BIND \_ PARAMETERS**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 **ActivePorts** 成员中提供了所有当前活动端口的列表。

以下主题介绍如何处理端口 PnP 事件：

[处理端口激活 PnP 事件](handling-the-port-activation-pnp-event.md)

[处理端口停用 PnP 事件](handling-the-port-deactivation-pnp-event.md)

 

