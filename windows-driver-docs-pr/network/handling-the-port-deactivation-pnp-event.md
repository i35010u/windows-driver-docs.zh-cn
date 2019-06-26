---
title: 处理端口停用 PnP 事件
description: 处理端口停用 PnP 事件
ms.assetid: 0e3b10a7-5ab5-48e1-a5cc-c7bc6ce26410
keywords:
- 端口 WDK NDIS，即插即用事件通知
- NDIS 端口 WDK，即插即用事件通知
- 即插即用事件通知 WDK NDIS 端口
- 停用的即插即用事件 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4431c2e014638888b5e92915af4b53009fbfe019
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381325"
---
# <a name="handling-the-port-deactivation-pnp-event"></a>处理端口停用 PnP 事件





过量驱动程序必须处理**NetEventPortDeactivation**微型端口驱动程序会停用的 NDIS 端口即插即用事件。 若要通知有关端口停用事件的基础驱动程序，NDIS 传播端口停用从基础的微型端口驱动程序的即插即用事件。

协议驱动程序完成端口停用的即插即用事件的处理之前，必须确保已完成所有未完成的 OID 请求和与端口相关联的发送请求。 协议驱动程序完成即插即用事件后，该驱动程序必须确保它不会发出任何 OID 请求或该端口的发送请求。

微型端口驱动程序指定**NetEventPortDeactivation** PnP 中的事件代码[ **NET\_PNP\_事件\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)结构的*NetPnPEvent*参数对的调用中指向[ **NdisMNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismnetpnpevent)报表的某些端口已被函数停用。 微型端口驱动程序指定数组的 NDIS\_端口\_数字值，若要列出的已停用的端口。 有关数组的端口号的详细信息，请参阅[Deactivating NDIS 端口](deactivating-an-ndis-port.md)。

 

 





