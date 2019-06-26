---
title: 报告 NIC 的 LSOV2 TCP 数据包分段功能
description: 报告 NIC 的 LSOV2 TCP 数据包分段功能
ms.assetid: 2894c1a8-503f-4b53-8eb3-5c5eaea150db
keywords:
- LSOV2 WDK 网络
- 大型 TCP 数据包分段 WDK 网络
- 分段的大型 TCP 数据包 WDK 网络
- 任务卸载，WDK TCP/IP 传输，LSOV1 和 LSOV2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5150d267a568552ce7c5813abd52853039cdf74
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373279"
---
# <a name="reporting-a-nics-lsov2-tcp-packet-segmentation-capabilities"></a>报告 NIC 的 LSOV2 TCP 数据包分段功能





NDIS 微型端口驱动程序指定当前的大量发送卸载版本 2 (LSOV2) 中的 NIC 的 TCP 数据包分段配置[ **NDIS\_TCP\_LARGE\_发送\_将卸载\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)结构。微型端口驱动程序必须包括中的当前 LSOV2 配置[ **NDIS\_微型端口\_适配器\_卸载\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)结构。 微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数从[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数并传递中信息在 NDIS\_微型端口\_适配器\_卸载\_属性。

微型端口驱动程序必须报告 LSOV2 配置中的更改，如果有，请在[ **NDIS\_状态\_任务\_卸载\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状态指示。

中的查询响应[OID\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)，NDIS 包括 NDIS\_TCP\_大\_发送\_将卸载\_V2 中的结构[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload) NDIS 返回中的结构**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构。 NDIS 使用微型端口驱动程序提供的信息。

我们建议支持 LSOV2 硬件的微型端口驱动程序还应支持 LSOV1。 这种支持将启用要使用 LSOV1 如果 NDIS 5 的 TCP/IP 传输。*x*微型端口适配器上安装中间的驱动程序。 有关 LSOV1 功能的详细信息，请参阅[报告的 NIC LSOV1 TCP 数据包分段功能](reporting-a-nic-s-lsov1-tcp-packet-segmentation-capabilities.md)。

LSOV2 支持 IPv4 和 IPv6 数据包。 微型端口驱动程序必须指定以下信息适用于 IPv4 和 IPv6 中的[ **NDIS\_TCP\_LARGE\_发送\_卸载\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)结构：

-   封装设置，请在**封装**成员。 有关此成员的详细信息，请参阅中的备注部分[ **NDIS\_TCP\_LARGE\_发送\_卸载\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_large_send_offload_v2)。

-   TCP/IP 传输在中可以传递给一个大型的 TCP 数据包中的微型端口驱动程序的用户数据的最大字节数**MaxOffLoadSize**成员。

-   TCP/IP 传输可以将卸载它为分段的 nic 中之前，大型的 TCP 数据包必须能被整除的段的最小数目**MinSegmentCount**成员。

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

 






