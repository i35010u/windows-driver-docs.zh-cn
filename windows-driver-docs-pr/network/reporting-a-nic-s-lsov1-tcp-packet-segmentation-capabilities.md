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
ms.openlocfilehash: c1c2affddf996784e1b2aacf024db9905c3183ce
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217501"
---
# <a name="reporting-a-nics-lsov1-tcp-packet-segmentation-capabilities"></a>报告 NIC 的 LSOV1 TCP 数据包分段功能





NDIS 微型端口驱动程序在 [**ndis \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ V1**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1) 结构中指定 LSOV1 的当前大发送卸载版本 1 () TCP 数据包分段配置。微型端口驱动程序必须在 [**NDIS \_ 微型端口 \_ 适配器 \_ 卸载 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes) 结构中包含当前 LSOV1 卸载配置。 微型端口驱动程序从[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并传入 NDIS \_ 微型端口 \_ 适配器 \_ 卸载特性中的信息 \_ 。

小型端口驱动程序必须在 [**NDIS \_ 状态 \_ 任务 " \_ 卸载 \_ 当前 \_ 配置**](./ndis-status-task-offload-current-config.md) 状态指示" 中报告 LSOV1 配置中的更改。

为了响应[OID \_ tcp \_ 卸载的 \_ 当前 \_ 配置](./oid-tcp-offload-current-config.md)，ndis 在 ndis \_ \_ 卸载结构中包含 ndis tcp 大规模 \_ 发送 \_ 卸载 V1 结构，ndis 在 ndis \_ [** \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员中返回。 [** \_ **](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) NDIS 使用微型端口驱动程序提供的信息。

NDIS 支持大型发送卸载版本 2 (LSOV2) ，它是 LSO 的增强版本。 有关 LSOV2 功能的详细信息，请参阅 [报告 NIC 的 LSOV2 TCP 数据包分段功能](reporting-a-nic-s-lsov2-tcp-packet-segmentation-capabilities.md)。

微型端口驱动程序必须在 NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ V1 结构中指定以下信息：

-   封装设置，位于 **封装** 成员中。 有关此成员的详细信息，请参阅 [**NDIS \_ TCP \_ 大规模 \_ 发送 \_ 卸载 \_ V1**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v1)中的 "备注" 部分。

-   在 **MaxOffLoadSize** 成员中，tcp/ip 传输可传递给大 TCP 数据包中的微型端口驱动程序的用户数据的最大字节数。 最大大小不能超过64K 字节。

-   在 **MinSegmentCount** 成员中，tcp/ip 传输可将大 tcp 数据包卸载到 NIC 进行分段的最小段数数。

-   NIC 是否可以分段包含 TCP 选项的大型 TCP 数据包。

-   NIC 是否可以分段包含 IPv4 选项的大型 TCP 数据包。

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

