---
title: 报告硬件状态
description: 报告硬件状态
ms.assetid: d4572c6f-dc09-41c4-af5b-69482b458bef
keywords:
- WMI WDK 网络，报告硬件状态
- 微型端口驱动程序 WDK 网络，硬件状态
- NDIS 微型端口驱动程序 WDK，硬件状态
- 硬件状态 WDK 网络
- 状态信息 WDK NDIS 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9de7c0b72555158244fda52ff4ee0d6c47a5fdd1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842044"
---
# <a name="reporting-hardware-status"></a>报告硬件状态





无连接微型端口驱动程序通过调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)指示硬件状态更改到上层。 面向连接的微型端口驱动程序通过调用[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)指示更改。

**NdisM （Co） IndicateStatusEx**同时使用一般状态代码和缓冲区，其中包含特定于媒体的信息，这些信息会进一步定义状态更改的原因。 NDIS 将此状态更改报告给绑定协议驱动程序。 NDIS 不会解释状态代码或以其他方式截获状态代码。

微型端口驱动程序可以进行一个或多个此类调用。 但是，与 NDIS 的早期版本不同，微型端口驱动程序并不表示它已完成发送状态。 协议驱动程序或配置管理器可以根据需要记录状态或采取纠正措施。

[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)使用任何有效的 NDIS\_状态\_*Xxx*值。

微型端口驱动程序负责指示对协议或更高级别的驱动程序有意义的状态代码。 协议驱动程序将忽略它不感兴趣的任何状态值，或者在其操作上下文中没有意义的状态值。

微型端口驱动程序无法在其[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)、 [*MiniportInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_isr)、 [*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)或[*MiniportShutdownEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)函数的上下文中指明状态。

小型小型驱动程序还可以由上层驱动程序询问，或通过 NDIS 了解微型端口驱动程序的硬件状态。 如果面向连接的微型端口驱动程序的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数或面向连接的微型端口驱动程序的[**MINIPORTCOOIDREQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)函数接收 OID\_代\_硬件\_状态，则它会使用任何在 NDIS 中定义的适用状态值\_硬件\_状态。 这些状态值包括：

-   **NdisHardwareStatusReady**

-   **NdisHardwareStatusInitializing**

-   **NdisHardwareStatusReset**

-   **NdisHardwareStatusClosing**

-   **NdisHardwareStatusNotReady**

可以查询微型端口驱动程序，使 NDIS 可以在 NDIS 驱动程序的各层之间同步操作-例如，通过确定 NIC 是否已准备好接受数据包。

 

 





