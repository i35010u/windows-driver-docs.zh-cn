---
title: 管理 NDIS 端口
description: 管理 NDIS 端口
ms.assetid: 08bb6623-aa9f-483e-a3cd-7dea676f3478
keywords:
- 端口 WDK NDIS，管理
- NDIS 端口 WDK，管理
- 端口状态 WDK NDIS
- 端口号 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3e248c83563b76d1845c04901eaf1e79aaf8300
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218069"
---
# <a name="managing-an-ndis-port"></a>管理 NDIS 端口





感兴趣的 NDIS 驱动程序和用户模式应用程序可以管理 NDIS 端口。 NDIS 提供服务来帮助管理端口。

NDIS 通过发出关联的状态指示和 PnP 事件，通知感兴趣的 NDIS 驱动程序和端口状态更改的用户模式应用程序。

传递给 send 和 receive 函数的端口号标识发送操作的目标端口或接收指示的源端口。 同样，关联结构中的端口号会标识状态指示、OID 请求和 PnP 事件的端口。 有关端口号的详细信息，请参阅 [NDIS 端口简介](overview-of-ndis-ports.md)。

为了帮助管理 NDIS 端口，以下结构包括端口号：

<a href="" id="ndis-oid-request"></a>[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)  
介绍 OID 请求。

<a href="" id="ndis-status-indication"></a>[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)  
描述 NDIS 状态指示。

<a href="" id="net-pnp-event-notification"></a>[**NET \_ PNP \_ 事件 \_ 通知**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)  
介绍 PnP 事件通知。

本节包括：

[NDIS 端口发送和接收操作](ndis-port-send-and-receive-operations.md)

[NDIS 端口 OID 请求](ndis-port-oid-requests.md)

[处理 NDIS 端口状态指示](handling-ndis-ports-status-indications.md)

[处理 NDIS 端口 PnP 事件通知](handling-ndis-ports-pnp-event-notifications.md)

 

