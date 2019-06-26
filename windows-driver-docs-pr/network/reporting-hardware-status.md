---
title: 报告硬件状态
description: 报告硬件状态
ms.assetid: d4572c6f-dc09-41c4-af5b-69482b458bef
keywords:
- WMI WDK 连接网络、 报告的硬件状态
- 微型端口驱动程序 WDK 网络硬件状态
- NDIS 微型端口驱动程序 WDK，硬件状态
- 硬件状态 WDK 网络
- WDK NDIS 微型端口的状态信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fe22361ebf237630f7f4388471a4798fbb24607
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373261"
---
# <a name="reporting-hardware-status"></a>报告硬件状态





无连接的微型端口驱动程序通过调用指示硬件状态设置为较高的层中的更改[ **NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)。 面向连接的微型端口驱动程序通过调用指示更改[ **NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)。

**NdisM (Co) IndicateStatusEx**采用常规状态代码和包含进一步定义的状态更改的原因的特定于媒体的信息的缓冲区。 NDIS 报告此状态更改绑定协议驱动程序。 NDIS 不解释也否则截获的状态代码。

微型端口驱动程序可以使一个或多个此类调用。 但是，与早期版本的 NDIS，不同的微型端口驱动程序不指示它已完成发送状态。 协议驱动程序或配置管理器可以记录状态或采取纠正措施，根据需要。

[**NdisMCoIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)采用任何有效的 NDIS\_状态\_*Xxx*值。

微型端口驱动程序负责，该值指示能够理解的协议或更高级别驱动程序的状态代码。 协议驱动程序将忽略任何不关注或的没有意义其操作的上下文中的状态值。

微型端口驱动程序不能指示状态的上下文中其[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)， [ *MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_isr)， [ *MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)，或[ *MiniportShutdownEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)函数。

微型端口驱动程序可以也要询问的上层驱动程序或 NDIS 有关微型端口驱动程序的硬件状态。 当[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数的无连接的微型端口驱动程序或[ **MiniportCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)的函数面向连接的微型端口驱动程序收到 OID\_GEN\_硬件\_状态，因此它的响应与的 NDIS 中定义的适用状态值任何\_硬件\_状态. 这些状态的值包括：

-   **NdisHardwareStatusReady**

-   **NdisHardwareStatusInitializing**

-   **NdisHardwareStatusReset**

-   **NdisHardwareStatusClosing**

-   **NdisHardwareStatusNotReady**

可以查询微型端口驱动程序，以便 NDIS 可以同步操作层之间的 NDIS 驱动程序-例如，通过确定 NIC 是否已准备好接受数据包。

 

 





