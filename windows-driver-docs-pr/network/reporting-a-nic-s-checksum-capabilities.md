---
title: 报告 NIC 的校验和功能
description: 报告 NIC 的校验和功能
ms.assetid: a90f8d01-8318-44de-acf0-7903ef7e85e0
keywords:
- 任务卸载，WDK TCP/IP 传输，校验和任务
- 校验和任务 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e18d68432d9cc7f60d967c49318c0a808b5aed9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373296"
---
# <a name="reporting-a-nics-checksum-capabilities"></a>报告 NIC 的校验和功能





NIC 是否当前配置为计算和验证中的 IP、 TCP 和 UDP 校验和 NDIS 微型端口驱动程序报告[ **NDIS\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)结构。 微型端口驱动程序必须包括中的当前校验和卸载配置[ **NDIS\_微型端口\_适配器\_卸载\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes)结构。 微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数从[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数并传递中信息在 NDIS\_微型端口\_适配器\_卸载\_属性。

微型端口驱动程序必须报告当前校验和卸载配置中的更改，如果有，请在[ **NDIS\_状态\_任务\_卸载\_当前\_配置** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-task-offload-current-config)状态指示。

中的查询响应[OID\_TCP\_卸载\_当前\_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-offload-current-config)，NDIS 包括 NDIS\_TCP\_IP\_的校验和\_在卸载结构[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload) NDIS 返回中的结构**InformationBuffer**隶属[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构。 NDIS 使用微型端口驱动程序提供的信息。

微型端口驱动程序获取 IPv4 和 IPv6 发送和接收数据包的指示以下的校验和信息：

-   类型的校验和 （IP、 TCP 或 UDP），NIC 可以计算为发送数据包，并可以验证为接收数据包。

-   封装设置，请在**封装**成员。 有关此成员的详细信息，请参阅中的备注部分[ **NDIS\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)。

-   NIC 可以计算或验证 （或计算并验证） 数据包的校验和是否其 IP 标头将包含 IPv4 选项。

-   NIC 可以计算或验证 （或计算并验证） 的 IPv6 数据包校验和是否其 IP 标头将包含 IPv6 扩展标头。

-   NIC 可以计算或验证 （或计算并验证） 数据包的校验和是否其 TCP 报头包含 TCP 选项。

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

 






