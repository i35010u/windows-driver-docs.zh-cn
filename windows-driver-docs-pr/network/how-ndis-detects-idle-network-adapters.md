---
title: NDIS 如何检测空闲的网络适配器
description: NDIS 如何检测空闲的网络适配器
ms.assetid: 1FF01B0B-9826-4467-8071-D26CA5E5EF4F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3603e7cf60020b438276247f05a12432a06e20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360824"
---
# <a name="how-ndis-detects-idle-network-adapters"></a>NDIS 如何检测空闲的网络适配器


微型端口驱动程序已启用后 NDIS 选择性挂起和已注册其处理程序函数、 NDIS 监视的网络适配器的 I/O 活动，如下所示：

-   NDIS 监视微型端口驱动程序注册通过 I/O 处理程序函数的调用[ **NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)和[ **NDIS\_微型端口\_PNP\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)结构。 例如，NDIS 监视对微型端口驱动程序调用[ *MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)或[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)以确定是否在任何包的 I/O 活动中涉及该驱动程序。

-   NDIS 还监视的调用[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)并[ **NdisDirectOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisdirectoidrequest)所做的过量协议驱动程序。

    **请注意**  NDIS 监视仅这些对象基础的微型端口驱动程序的未直接由 NDIS 标识符 (OID) 请求。

     

NDIS 确定网络适配器处于空闲状态，如果它不会检测空闲超时时间的适配器上的任何活动。 此超时期限的持续时间指定的值 **\*SSIdleTimeout**标准化 INF 关键字。 有关此关键字的详细信息，请参阅[NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)。

网络适配器已进入空闲状态后，NDIS 启动选择性挂起操作。 通过此操作，网络适配器挂起通过转换为低功耗状态。

NDIS 开始这选择性挂起操作通过向微型端口驱动程序发出的空闲通知。 NDIS 将这是通过调用在驱动程序[ *MiniportIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_idle_notification)处理程序函数。 有关微型端口驱动程序如何处理此通知的详细信息，请参阅[处理 NDIS 选择性挂起空闲通知](handling-the-ndis-selective-suspend-idle-notification.md)。

如果 NDIS 检测到，通过覆盖驱动程序发出 I/O 请求到的网络适配器或适配器向唤醒事件发出信号，NDIS 取消空闲通知。 NDIS 将这是通过调用微型端口驱动程序[ *MiniportCancelIdleNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_idle_notification)处理程序函数。

有关如何 NDIS 取消空闲通知的详细信息，请参阅[取消 NDIS 挂起空闲选择性通知](canceling-the-ndis-selective-suspend-idle-notification.md)。

有关如何微型端口驱动程序完成空闲通知的详细信息，请参阅[完成 NDIS 挂起空闲选择性通知](completing-the-ndis-selective-suspend-idle-notification.md)。

 

 





