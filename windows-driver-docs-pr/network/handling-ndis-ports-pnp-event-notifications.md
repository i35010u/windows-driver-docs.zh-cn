---
title: NDIS 端口 PnP 事件通知
description: NDIS 端口 PnP 事件通知
ms.assetid: 2f542b62-43a0-42fa-b72d-f789e029d3f0
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
ms.openlocfilehash: d75ccf66dc32c5bd9912e996d3b55b194c372715
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842586"
---
# <a name="ndis-ports-pnp-event-notifications"></a>NDIS 端口 PnP 事件通知

当激活或停用端口时，NDIS 转发 PnP 事件以通知过量驱动程序。 分配端口时，NDIS 和微型端口驱动程序不会生成 PnP 事件。 微型端口驱动程序通知 NDIS：已使用**NetEventPortActivation** PnP 事件激活端口，微型端口驱动程序生成**NetEventPortDeactivation** PnP 事件，以通知 NDIS，某些端口已被停用。

当 NDIS 调用协议驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，ndis 将在[**ndis\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构 *的 ActivePorts 成员中提供所有当前活动端口的列表。BindParameters*参数。

以下主题介绍如何处理端口 PnP 事件：

[处理端口激活 PnP 事件](handling-the-port-activation-pnp-event.md)

[处理端口停用 PnP 事件](handling-the-port-deactivation-pnp-event.md)

 

 





