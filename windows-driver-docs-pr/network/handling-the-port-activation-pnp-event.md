---
title: 处理端口激活 PnP 事件
description: 处理端口激活 PnP 事件
ms.assetid: 433018bf-daf5-4ea1-be3f-63349558f6b7
keywords:
- 端口 WDK NDIS，PnP 事件通知
- NDIS 端口 WDK，PnP 事件通知
- PnP 事件通知 WDK NDIS 端口
- 激活 PnP 事件 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bf5bf8c05e2f519091da5b9582f2706348c79d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842553"
---
# <a name="handling-the-port-activation-pnp-event"></a>处理端口激活 PnP 事件





当微型端口驱动程序激活 NDIS 端口时，过量驱动程序必须处理**NetEventPortActivation** PnP 事件。 在激活默认端口之前，NDIS 不会启动协议驱动程序和微型端口适配器之间的绑定。 因此，协议驱动程序应将对其[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数的调用视为默认端口处于活动状态的通知。

协议驱动程序不得在任何 NDIS 请求中使用端口号，除非驱动程序接收到端口处于活动状态的通知，无论是通过绑定参数还是通过**NetEventPortActivation** PnP 事件。

当微型端口驱动程序激活一些端口之后，NDIS 将生成端口激活 PnP 事件。 （微型端口驱动程序指定[**NET\_pnp\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)中的**NetEventPortActivation** PNP 事件代码\_通知结构， *NetPnPEvent*参数在调用[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)时指向激活 NDIS 端口。）

微型端口驱动程序可以通过使用[**NDIS\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port)结构中的**下一个**成员链接多个 ndis\_端口结构，来指示在一个 PnP 通知中激活多个端口。 有关 NDIS\_端口结构的链接列表的详细信息，请参阅[激活 Ndis 端口](activating-an-ndis-port.md)。

当微型端口停用某个端口时，NDIS 会将**NetEventPortDeactivation** PnP 事件生成到绑定协议驱动程序。 有关**NetEventPortDeactivation** PnP 事件的详细信息，请参阅[处理端口停用 pnp 事件](handling-the-port-deactivation-pnp-event.md)。

 

 





