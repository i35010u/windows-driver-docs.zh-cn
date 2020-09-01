---
title: NDIS 如何检测空闲的网络适配器
description: NDIS 如何检测空闲的网络适配器
ms.assetid: 1FF01B0B-9826-4467-8071-D26CA5E5EF4F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ac1583ccfdf224b1b91c67158549535d2ddc4c2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209735"
---
# <a name="how-ndis-detects-idle-network-adapters"></a>NDIS 如何检测空闲的网络适配器


在微型端口驱动程序启用 NDIS 选择性挂起并注册其处理程序函数后，NDIS 会按以下方式监视网络适配器的 i/o 活动：

-   NDIS 监视对 i/o 处理程序函数的调用，微型端口驱动程序通过 [**ndis \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics) 和 [**ndis \_ 微型端口 \_ PNP \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_pnp_characteristics) 结构注册。 例如，NDIS 监视对微型端口驱动程序的 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 或 [*MiniportReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists) 的调用，以确定是否在任何数据包 i/o 活动中涉及该驱动程序。

-   NDIS 还监视过量协议驱动程序发出的 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 和 [**NdisDirectOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdirectoidrequest) 调用。

    **注意**   NDIS 仅监视 (OID) 请求不由 NDIS 直接处理的基础微型端口驱动程序的对象标识符。

     

NDIS 确定网络适配器在空闲超时期限内未检测到适配器上的任何活动时处于空闲状态。 此超时期限的持续时间由** \* SSIDLETIMEOUT**标准化 INF 关键字的值指定。 有关此关键字的详细信息，请参阅 [用于 NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)。

网络适配器进入空闲状态后，NDIS 将启动选择性挂起操作。 完成此操作后，网络适配器将被转换为低功耗状态。

NDIS 通过向微型端口驱动程序发出空闲通知来开始此选择性挂起操作。 NDIS 通过调用驱动程序的 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification) 处理程序函数来实现此功能。 有关微型端口驱动程序如何处理此通知的详细信息，请参阅 [处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)。

如果 NDIS 检测到对网络适配器发出的 i/o 请求是从覆盖驱动程序发出的，或者如果适配器发出唤醒事件，NDIS 将取消空闲通知。 NDIS 通过调用微型端口驱动程序的 [*MiniportCancelIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_idle_notification) 处理程序函数来实现此功能。

有关 NDIS 如何取消空闲通知的详细信息，请参阅 [取消 Ndis 选择性挂起空闲通知](canceling-the-ndis-selective-suspend-idle-notification.md)。

有关微型端口驱动程序如何完成空闲通知的详细信息，请参阅 [完成 NDIS 选择性挂起空闲通知](completing-the-ndis-selective-suspend-idle-notification.md)。

 

