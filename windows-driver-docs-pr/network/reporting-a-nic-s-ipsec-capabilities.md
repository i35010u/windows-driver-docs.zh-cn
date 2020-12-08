---
title: 报告 NIC 的 IPsec 功能
description: 报告 NIC 的 IPsec 功能
keywords:
- 任务卸载 WDK TCP/IP 传输，IPsec 任务
- IPsec 卸载 WDK TCP/IP 传输，功能
- IPsec 卸载 WDK TCP/IP 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b56bdc3634e8e663c361ddf3b2597843ebd647f8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815901"
---
# <a name="reporting-a-nics-ipsec-capabilities"></a>报告 NIC 的 IPsec 功能

\[IPsec 任务卸载功能已弃用，不应使用。\]




NDIS 微型端口驱动程序指定当前 Internet 协议安全 (IPsec) 在 [**NDIS \_ IPsec \_ 卸载 \_ V1**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1) 结构中卸载 NIC 的配置。微型端口驱动程序必须在 [**NDIS \_ 微型端口 \_ 适配器 \_ 卸载 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes) 结构中包含当前 IPsec 卸载配置。 微型端口驱动程序从 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并传入 NDIS \_ 微型端口 \_ 适配器 \_ 卸载特性中的信息 \_ 。

小型端口驱动程序必须在 [**NDIS \_ 状态 \_ 任务 " \_ 卸载 \_ 当前 \_ 配置**](./ndis-status-task-offload-current-config.md) 状态指示" 中报告 IPsec 卸载功能的更改（如果有）。

为了响应 [OID \_ TCP \_ 卸载的 \_ 当前 \_ 配置](./oid-tcp-offload-current-config.md)，ndis 在 ndis \_ \_ 卸载结构中包含 ndis IPSEC 卸载 \_ V1 结构， [**\_**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)该结构在 ndis [**\_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员中返回。 NDIS 使用微型端口驱动程序提供的信息。

微型端口驱动程序指示 NDIS \_ IPSEC \_ 卸载 V1 结构中的以下信息 \_ ：

-   封装设置，位于 **封装** 成员中。 有关此成员的详细信息，请参阅 [**NDIS \_ IPSEC \_ 卸载 \_ V1**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ipsec_offload_v1)中的 "备注" 部分。

-   NIC 是否可以在数据包上执行合并 IPsec 操作，即，NIC 是否可以使用以下格式处理同时包含 authentication 标头 (AH) 和封装式安全负载 (ESP) 的数据包：

    \[IP \] \[ AH \] \[ ESP \] \[ 剩余数据包\]

-   NIC 是否可以在发送和接收数据包的传输模式部分和隧道模式部分执行 IP 安全处理。 数据包的传输模式部分适用于端到端安全关联，而数据包的隧道模式部分则属于隧道安全关联。

-   如果数据包的 IP 标头包含 IP 选项，NIC 是否可以在数据包上执行 IP 安全操作。

微型端口驱动程序指定 NIC 的以下功能，以便计算或验证 (或计算和验证 AH 负载和身份验证信息) 加密校验和：

-    (MD5 或 SHA 1) NIC 可以使用的完整性算法

-   NIC 是否可以处理 AH 安全负载：
    -   数据包的传输模式部分
    -   数据包的隧道模式部分
    -   发送数据包
    -   接收数据包

微型端口驱动程序指定 NIC 的以下功能来处理 ESP 负载：

-   机密性算法 (DES、三重 DES，或 NIC 可以使用的两种) 

-   NIC 是否支持 null 加密 (也就是说，没有加密但具有身份验证哈希的 ESP 有效负载) 

-   NIC 是否可以对执行 ESP 处理：
    -   数据包的传输模式部分
    -   数据包的隧道模式部分
    -   发送数据包
    -   接收数据包

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

