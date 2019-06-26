---
title: 处理端口激活 PnP 事件
description: 处理端口激活 PnP 事件
ms.assetid: 433018bf-daf5-4ea1-be3f-63349558f6b7
keywords:
- 端口 WDK NDIS，即插即用事件通知
- NDIS 端口 WDK，即插即用事件通知
- 即插即用事件通知 WDK NDIS 端口
- 激活即插即用事件 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 780918f40f98fb5a6523fbf2764848f7cb35de3b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381331"
---
# <a name="handling-the-port-activation-pnp-event"></a>处理端口激活 PnP 事件





过量驱动程序必须处理**NetEventPortActivation**微型端口驱动程序将激活 NDIS 端口即插即用事件。 NDIS 并不会启动协议驱动程序和微型端口适配器之间的绑定，直到已激活的默认端口。 因此，协议驱动程序应将调用其[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数作为默认端口处于活动状态的通知。

除非驱动程序收到通知的端口已处于活动状态，则可通过绑定参数或协议驱动程序不得 NDIS 的任何请求中使用的端口号**NetEventPortActivation**即插即用事件。

NDIS 生成端口激活即插即用事件后的微型端口驱动程序将激活某些端口。 (微型端口驱动程序指定**NetEventPortActivation** PnP 中的事件代码[ **NET\_PNP\_事件\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)结构的*NetPnPEvent*参数对的调用中指向[ **NdisMNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismnetpnpevent)激活 NDIS 端口。)

微型端口驱动程序可以通过使用指示的一个即插即用通知中的多个端口的激活**下一步**中的成员[ **NDIS\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port)结构链接多个 NDIS\_端口结构。 详细了解链接列表的 NDIS\_移植结构，请参阅[正在激活 NDIS 端口](activating-an-ndis-port.md)。

生成 NDIS **NetEventPortDeactivation**绑定的协议驱动程序微型端口将停用某些端口时即插即用事件。 有关详细信息**NetEventPortDeactivation** PnP 事件，请参阅[处理端口停用的即插即用事件](handling-the-port-deactivation-pnp-event.md)。

 

 





