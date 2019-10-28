---
title: 报告 NIC 的校验和功能
description: 报告 NIC 的校验和功能
ms.assetid: a90f8d01-8318-44de-acf0-7903ef7e85e0
keywords:
- 任务卸载 WDK TCP/IP 传输，校验和任务
- 校验和任务 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f714960cf14af55d3848ade613fa69290bc4fae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842057"
---
# <a name="reporting-a-nics-checksum-capabilities"></a>报告 NIC 的校验和功能





NDIS 微型端口驱动程序报告 NIC 当前是否配置为在 NDIS 中计算和验证 IP、TCP 和 UDP 校验和[ **\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)结构。 微型端口驱动程序必须在[**NDIS\_微型端口\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)中包含当前校验和卸载配置，\_卸载\_属性结构。 微型端口驱动程序从[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并将 NDIS\_微型端口\_适配器中的信息传入\_卸载\_特性。

微型端口驱动程序必须在[**NDIS\_状态\_任务\_卸载\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状态指示中报告当前校验和卸载配置中的更改（如果有）。

为了响应[OID\_tcp\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)，Ndis 在[**ndis\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构中包含 ndis\_的 tcp\_NDIS [ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员返回。\_\_ NDIS 使用微型端口驱动程序提供的信息。

微型端口驱动程序指示 IPv4 和 IPv6 发送和接收数据包的以下校验和信息：

-   NIC 可计算用于发送数据包并可验证接收数据包的校验和类型（IP、TCP 或 UDP）。

-   封装设置，位于**封装**成员中。 有关此成员的详细信息，请参阅 NDIS 中的 "备注" 部分[ **\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)。

-   NIC 是否可以计算或验证（或计算和验证）其 IP 标头包含 IPv4 选项的数据包的校验和。

-   NIC 是否可以计算或验证（或计算和验证）其 IP 标头包含 IPv6 扩展标头的 IPv6 数据包的校验和。

-   NIC 是否可以计算或验证（或计算和验证）其 TCP 标头包含 TCP 选项的数据包的校验和。

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

 






