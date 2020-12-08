---
title: 报告 NIC 的 LSOV2 TCP 数据包分段功能
description: 报告 NIC 的 LSOV2 TCP 数据包分段功能
keywords:
- LSOV2 WDK 网络
- 大型 TCP 数据包分段 WDK 网络
- 大 TCP 数据包的分段 WDK 网络
- 任务卸载 WDK TCP/IP 传输、LSOV1 和 LSOV2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16293d36418e93a67e493796f1565431c3664a80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808021"
---
# <a name="reporting-a-nics-lsov2-tcp-packet-segmentation-capabilities"></a>报告 NIC 的 LSOV2 TCP 数据包分段功能





NDIS 微型端口驱动程序在 [**ndis \_ tcp \_ 大规模 \_ 发送 \_ 卸载 \_ V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2) 结构中指定 LSOV2 的当前大发送卸载版本 2 () TCP 数据包分段配置。微型端口驱动程序必须在 [**NDIS \_ 微型端口 \_ 适配器 \_ 卸载 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes) 结构中包含当前的 LSOV2 配置。 微型端口驱动程序从 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并传入 NDIS \_ 微型端口 \_ 适配器 \_ 卸载特性中的信息 \_ 。

小型端口驱动程序必须在 [**NDIS \_ 状态 \_ 任务 " \_ 卸载 \_ 当前 \_ 配置**](./ndis-status-task-offload-current-config.md) 状态指示" 中报告 LSOV2 配置中的更改。

为了响应 [OID \_ tcp \_ 卸载的 \_ 当前 \_ 配置](./oid-tcp-offload-current-config.md)查询，ndis 在 ndis \_ OID 请求结构的 InformationBuffer 成员中包含 ndis TCP \_ 大规模 \_ 发送 \_ 卸载 \_ V2 结构。 [**\_**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) [**\_ \_**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) **InformationBuffer** NDIS 使用微型端口驱动程序提供的信息。

建议支持 LSOV2 硬件的微型端口驱动程序还应支持 LSOV1。 如果 NDIS 5，此支持将使 TCP/IP 传输能使用 LSOV1。*x* 中间驱动程序安装在微型端口适配器上。 有关 LSOV1 功能的详细信息，请参阅 [报告 NIC 的 LSOV1 TCP 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)。

LSOV2 支持 IPv4 和 IPv6 数据包。 微型端口驱动程序必须在 [**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2) 结构中为 IPv4 和 IPv6 指定以下信息：

-   封装设置，位于 **封装** 成员中。 有关此成员的详细信息，请参阅 [**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ V2**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)中的 "备注" 部分。

-   在 **MaxOffLoadSize** 成员中，tcp/ip 传输可传递给大 TCP 数据包中的微型端口驱动程序的用户数据的最大字节数。

-   在 **MinSegmentCount** 成员中，tcp/ip 传输可将大 tcp 数据包卸载到 NIC 进行分段的最小段数数。

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

