---
title: 报告 NIC 的 LSOV1 TCP 数据包分段功能
description: 报告 NIC 的 LSOV1 TCP 数据包分段功能
ms.assetid: 976f5943-a50e-413b-8520-e280b04122f9
keywords:
- LSOV1 WDK 网络
- 大型 TCP 数据包分段 WDK 网络
- 大 TCP 数据包的分段 WDK 网络
- 任务卸载 WDK TCP/IP 传输、LSOV1 和 LSOV2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0795f42c6ae5e5c82d427e47c429c39d0eaaa56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842049"
---
# <a name="reporting-a-nics-lsov1-tcp-packet-segmentation-capabilities"></a>报告 NIC 的 LSOV1 TCP 数据包分段功能





NDIS 微型端口驱动程序在[**ndis\_tcp\_大型\_发送\_卸载\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)结构中指定当前的大型发送卸载版本1（LSOV1） tcp 数据包分段配置。微型端口驱动程序必须在[**NDIS\_微型端口\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)中包含当前 LSOV1 卸载配置，\_卸载\_属性结构。 微型端口驱动程序从[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并将 NDIS\_微型端口\_适配器中的信息传入\_卸载\_特性。

微型端口驱动程序必须在[**NDIS\_状态\_任务\_卸载\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状态指示中报告 LSOV1 配置中的更改（如果有）。

为了响应[OID\_tcp\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)，Ndis 在[**ndis\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)中包含 ndis\_TCP\_\_\_卸载ndis [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员中返回的结构。 NDIS 使用微型端口驱动程序提供的信息。

NDIS 支持大型发送卸载版本2（LSOV2），这是 LSO 的增强版本。 有关 LSOV2 功能的详细信息，请参阅[报告 NIC 的 LSOV2 TCP 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)。

微型端口驱动程序必须在 NDIS\_TCP\_大型\_发送\_卸载\_V1 结构中指定以下信息：

-   封装设置，位于**封装**成员中。 有关此成员的详细信息，请参阅 NDIS 中的 "备注" 部分[ **\_TCP\_大型\_发送\_卸载\_V1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)。

-   在**MaxOffLoadSize**成员中，tcp/ip 传输可传递给大 TCP 数据包中的微型端口驱动程序的用户数据的最大字节数。 最大大小不能超过64K 字节。

-   在**MinSegmentCount**成员中，tcp/ip 传输可将大 tcp 数据包卸载到 NIC 进行分段的最小段数数。

-   NIC 是否可以分段包含 TCP 选项的大型 TCP 数据包。

-   NIC 是否可以分段包含 IPv4 选项的大型 TCP 数据包。

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

 






