---
title: NDIS 端口 PnP 事件通知
description: NDIS 端口 PnP 事件通知
ms.assetid: 2f542b62-43a0-42fa-b72d-f789e029d3f0
keywords:
- 端口 WDK NDIS, PnP 事件通知
- NDIS 端口 WDK, PnP 事件通知
- PnP 事件通知 WDK NDIS 端口
- 事件通知 WDK 网络
- 通知 WDK 网络
- 通知 WDK PnP, NDIS 端口
- 事件 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 331bc8ca32faad606225645ba75f447d90bf57b1
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565759"
---
# <a name="ndis-ports-pnp-event-notifications"></a>NDIS 端口 PnP 事件通知

当激活或停用端口时, NDIS 转发 PnP 事件以通知过量驱动程序。 分配端口时, NDIS 和微型端口驱动程序不会生成 PnP 事件。 微型端口驱动程序通知 NDIS: 已使用**NetEventPortActivation** PnP 事件激活端口, 微型端口驱动程序生成**NetEventPortDeactivation** PnP 事件, 以通知 NDIS, 某些端口已被停用。

当 ndis 调用协议驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数时, ndis 会提供[**ndis\_\_绑定参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)结构 *的 ActivePorts 成员中所有当前处于活动状态的端口的列表,BindParameters*参数。

以下主题介绍如何处理端口 PnP 事件:

[处理端口激活 PnP 事件](handling-the-port-activation-pnp-event.md)

[处理端口停用 PnP 事件](handling-the-port-deactivation-pnp-event.md)

 

 





