---
title: 报告 NIC 的 LSOV2 TCP 数据包分段功能
description: 报告 NIC 的 LSOV2 TCP 数据包分段功能
ms.assetid: 2894c1a8-503f-4b53-8eb3-5c5eaea150db
keywords:
- LSOV2 WDK 网络
- 大型 TCP 数据包分段 WDK 网络
- 大 TCP 数据包的分段 WDK 网络
- 任务卸载 WDK TCP/IP 传输、LSOV1 和 LSOV2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f3a7deeeeda1bd4910128ff6e2d1222a778ba83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842047"
---
# <a name="reporting-a-nics-lsov2-tcp-packet-segmentation-capabilities"></a>报告 NIC 的 LSOV2 TCP 数据包分段功能





NDIS 微型端口驱动程序在[**ndis\_tcp\_大型\_发送\_卸载\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)结构中指定当前大型发送卸载版本2（LSOV2） tcp 数据包分段配置。微型端口驱动程序必须在[**NDIS\_微型端口\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)中包含当前的 LSOV2 配置，\_卸载\_属性结构。 微型端口驱动程序从[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并将 NDIS\_微型端口\_适配器中的信息传入\_卸载\_特性。

微型端口驱动程序必须在[**NDIS\_状态\_任务\_卸载\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状态指示中报告 LSOV2 配置中的更改（如果有）。

为了响应[OID\_tcp\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)，Ndis 在[**ndis\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)中包含 ndis\_tcp\_\_\_卸载ndis [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员中返回的结构。 NDIS 使用微型端口驱动程序提供的信息。

建议支持 LSOV2 硬件的微型端口驱动程序还应支持 LSOV1。 如果 NDIS 5，此支持将使 TCP/IP 传输能使用 LSOV1。*x*中间驱动程序安装在微型端口适配器上。 有关 LSOV1 功能的详细信息，请参阅[报告 NIC 的 LSOV1 TCP 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)。

LSOV2 支持 IPv4 和 IPv6 数据包。 微型端口驱动程序必须在[**NDIS\_TCP\_大型\_发送\_卸载\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)结构中指定以下信息：

-   封装设置，位于**封装**成员中。 有关此成员的详细信息，请参阅 NDIS 中的 "备注" 部分[ **\_TCP\_大型\_发送\_卸载\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)。

-   在**MaxOffLoadSize**成员中，tcp/ip 传输可传递给大 TCP 数据包中的微型端口驱动程序的用户数据的最大字节数。

-   在**MinSegmentCount**成员中，tcp/ip 传输可将大 tcp 数据包卸载到 NIC 进行分段的最小段数数。

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

 






