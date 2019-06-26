---
title: 处理 NDIS 端口 PnP 事件通知
description: 处理 NDIS 端口 PnP 事件通知
ms.assetid: 2f542b62-43a0-42fa-b72d-f789e029d3f0
keywords:
- 端口 WDK NDIS，即插即用事件通知
- NDIS 端口 WDK，即插即用事件通知
- 即插即用事件通知 WDK NDIS 端口
- 事件通知 WDK 网络
- 通知 WDK 网络
- 通知 WDK 即插即用，NDIS 端口
- 事件 WDK networkin
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69aca41a9c7c18db1400ffb840ca167a594b202a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379820"
---
# <a name="handling-ndis-ports-pnp-event-notifications"></a>处理 NDIS 端口 PnP 事件通知





NDIS 转发即插即用事件以在端口是激活或停用时通知基础驱动程序。 NDIS 和微型端口驱动程序不会生成一个即插即用事件时分配一个端口。 微型端口驱动程序通知端口已激活与的 NDIS **NetEventPortActivation**即插即用事件和微型端口驱动程序生成**NetEventPortDeactivation** ，有些通知 NDIS 的即插即用事件已停用的端口。

当调用 NDIS [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)协议驱动程序，NDIS 函数提供了一系列中的所有当前活动端口**ActivePorts** 的成员[**NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)结构在*BindParameters*参数。

以下主题介绍如何处理端口即插即用事件：

[处理端口激活即插即用事件](handling-the-port-activation-pnp-event.md)

[处理端口停用的即插即用事件](handling-the-port-deactivation-pnp-event.md)

 

 





