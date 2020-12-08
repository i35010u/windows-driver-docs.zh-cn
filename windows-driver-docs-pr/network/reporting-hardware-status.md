---
title: 报告硬件状态
description: 报告硬件状态
keywords:
- WMI WDK 网络，报告硬件状态
- 微型端口驱动程序 WDK 网络，硬件状态
- NDIS 微型端口驱动程序 WDK，硬件状态
- 硬件状态 WDK 网络
- 状态信息 WDK NDIS 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c18075e50a6c5a6117046468f8a2652d92b7000
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815899"
---
# <a name="reporting-hardware-status"></a>报告硬件状态





无连接微型端口驱动程序通过调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)指示硬件状态更改到上层。 面向连接的微型端口驱动程序通过调用 [**NdisMCoIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)指示更改。

**NdisM (Co) IndicateStatusEx** 都采用常规状态代码和缓冲区，其中包含特定于媒体的信息，这些信息会进一步定义状态更改的原因。 NDIS 将此状态更改报告给绑定协议驱动程序。 NDIS 不会解释状态代码或以其他方式截获状态代码。

微型端口驱动程序可以进行一个或多个此类调用。 但是，与 NDIS 的早期版本不同，微型端口驱动程序并不表示它已完成发送状态。 协议驱动程序或配置管理器可以根据需要记录状态或采取纠正措施。

[**NdisMCoIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)采用任意有效 \_ 的 NDIS 状态 \_ *Xxx* 值。

微型端口驱动程序负责指示对协议或更高级别的驱动程序有意义的状态代码。 协议驱动程序将忽略它不感兴趣的任何状态值，或者在其操作上下文中没有意义的状态值。

微型端口驱动程序无法在其 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)、 [*MiniportInterrupt*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)、 [*MiniportHaltEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)或 [*MiniportShutdownEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown) 函数的上下文中指明状态。

小型小型驱动程序还可以由上层驱动程序询问，或通过 NDIS 了解微型端口驱动程序的硬件状态。 在无连接微型端口驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数或面向连接的微型端口驱动程序的 [**MINIPORTCOOIDREQUEST**](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request) 函数接收 OID 生成 \_ \_ 硬件 \_ 状态时，它会使用在 NDIS 硬件状态中定义的任何适用状态值进行响应 \_ \_ 。 这些状态值包括：

-   **NdisHardwareStatusReady**

-   **NdisHardwareStatusInitializing**

-   **NdisHardwareStatusReset**

-   **NdisHardwareStatusClosing**

-   **NdisHardwareStatusNotReady**

可以查询微型端口驱动程序，使 NDIS 可以在 NDIS 驱动程序的各层之间同步操作-例如，通过确定 NIC 是否已准备好接受数据包。

 

