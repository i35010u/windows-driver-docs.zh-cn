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
ms.openlocfilehash: ddb816426be0a7c31723a55ccb0eeaac52de8fb5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356170"
---
# <a name="managing-an-ndis-port"></a>管理 NDIS 端口





感的 NDIS 驱动程序和用户模式应用程序可以管理 NDIS 端口。 NDIS 提供服务来帮助管理端口。

NDIS 通过发出的关联的状态指示和即插即用事件通知的兴趣的 NDIS 驱动程序和用户模式应用程序的端口状态更改。

传递来发送和接收函数的端口号标识发送操作的目标端口或接收指示的源端口。 同样，关联的结构中的端口号标识状态指示、 OID 请求和即插即用事件的端口。 有关端口号的详细信息，请参阅[NDIS 端口简介](overview-of-ndis-ports.md)。

若要帮助管理 NDIS 端口，以下结构包括端口号：

<a href="" id="ndis-oid-request"></a>[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)  
介绍 OID 请求。

<a href="" id="ndis-status-indication"></a>[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)  
介绍 NDIS 状态指示。

<a href="" id="net-pnp-event-notification"></a>[**NET\_PNP\_EVENT\_NOTIFICATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)  
介绍即插即用事件通知。

本部分包括：

[NDIS 端口发送和接收操作](ndis-port-send-and-receive-operations.md)

[NDIS 端口 OID 请求](ndis-port-oid-requests.md)

[处理 NDIS 端口状态指示](handling-ndis-ports-status-indications.md)

[处理 NDIS 端口 PnP 事件通知](handling-ndis-ports-pnp-event-notifications.md)

 

 





